---
layout: post
slug: conditional-loading-of-doctrine-mappings
title: "Conditional loading of Doctrine mappings"
date: "2022-12-01"
categories: [PHP, Symfony]
authors: [iain]
draft: false
---
One of the core principles of Parthenon is to provide a performant and scalable foundation to build upon. To allow for that modules have to be enabled and without being enabled they should have no effect to the application. With there being many parts of Parthenon that use Doctrine ORM and/or ODM, it's important that these aren't loaded unless that module is enabled. Here we'll explain how we handle this and why we handle it in that way.

## Understanding Symfony Doctrine Autoloading

Symfony has added support for automatically detecting doctrine ORM configuration for a bundle. This is very useful as it allows you to not worry about handling it yourself. 

The way it works is when your bundle is added to a Symfony application it will look for a directory in the bundle source directory that directory is `resources/doctrine`. When it finds that directory it'll load all the files that end with `.orm.xml` into the doctrine mapping configuration.

### Downsides

The downsides of this, for Parthenon, are that it'll load all the files, the namespace is guessed, and It also needs the mapping files to be in the root of that directory. Loading all the files would remove the ability to only load doctrine mappings when that module is enabled. The namespace for the entities are all different as each module has its own namespace. And having all the mapping files in the same directory would remove the ability to have them neatly organised.

To work around this Parthenon has its doctrine mappings in the `resources/doctrine-mappings` directory and then stored into sub-directories based on the module they are for.

## Understanding Doctrine Compiler Passes

Doctrine ORM/ODM bundles come with compiler passes. A quick explanation of what compiler passes are is they allow you to execute code upon the compiling of the Symfony service container. This allows you to add more advanced configurations programmatically. These are added in the `build` method of the bundle class. One of the compiler passes is the load mapping compiler pass. These allow you to define the directory and namespace of the mapping files. 

These compiler passes have a functionality that allows you to define if they're enabled based on the service container having a parameter. Not that the parameter has a value just that the parameter exists. So if you have a parameter that is a boolean value that says if the module is enabled it would always trigger the compiler pass. This means that instead when the module is enabled a special parameter is set to show that it's enabled. When it's not enabled that parameter does not exist. This is done because it's possible that you may only realise you need to enable the mappings based on the bundle configuration which isn't processed until later on in the service container compilation process at which point it's no longer possible to add compiler passes.

## What we do

We use Doctrine ORM/ODM compiler passes to define the directory of the XML files and the namespace these XML files represent. And add these to a compiler pass in the bundle file and use the `enabledParameter` option in the compiler pass to decide when these are enabled. Each module sets a parameter `parthenon_{moduleName}_enabled` when it's enabled.

### Example code from Bundle

```php
<?PHP

namespace Parthenon;


use Doctrine\Bundle\DoctrineBundle\DependencyInjection\Compiler\DoctrineOrmMappingsPass;
use Doctrine\Bundle\MongoDBBundle\DependencyInjection\Compiler\DoctrineMongoDBMappingsPass;
use Symfony\Component\DependencyInjection\ContainerBuilder;
use Symfony\Component\HttpKernel\Bundle\Bundle;

class ParthenonBundle extends Bundle
{
    public function build(ContainerBuilder $container)
    {
        parent::build($container);
        // ...
        $this->handleAthenaDoctrine($container);
    }

    public function handleAthenaDoctrine(ContainerBuilder $containerBuilder) : void {

        $athenaMappings = [
            realpath(__DIR__.'/Resources/config/doctrine-mapping/Athena') => 'Parthenon\Athena\Entity',
        ];

        // This contains bundles that are loaded
        $bundles = $containerBuilder->getParameter('kernel.bundles');

        // Doctrine ORM Bundle
        if (isset($bundles['DoctrineBundle'])) {

            $containerBuilder->addCompilerPass(DoctrineOrmMappingsPass::createXmlMappingDriver($athenaMappings, ['parthenon.athena.orm'], enabledParameter: 'parthenon_athena_enabled'));
        }
        // Doctrine ODM Bundle
        if (isset($bundles['DoctrineMongoDBBundle'])) {
            $containerBuilder->addCompilerPass(DoctrineMongoDBMappingsPass::createXmlMappingDriver($athenaMappings, ['parthenon.athena.mongodb'], enabledParameter: 'parthenon_athena_enabled'));
        }
    }
    
