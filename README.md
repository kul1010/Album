Sample Album Module for Zend3
Introduction

After Zend 3 installation Clone this project into your ./module/ directory and enable it in your config/modules.config.php file at root folder.

return [
    'Zend\ServiceManager\Di',
    'Zend\Session',
    'Zend\Mvc\Plugin\Prg',
    'Zend\Mvc\Plugin\Identity',
    'Zend\Mvc\Plugin\FlashMessenger',
    'Zend\Mvc\Plugin\FilePrg',
    'Zend\Mvc\I18n',
    'Zend\Mvc\Console',
    'Zend\Log',
    'Zend\Form',
    'Zend\Db',
    'Zend\Cache',
    'ZendDeveloperTools',
    'Zend\Router',
    'Zend\Validator',
    'Application',
    'Album',//your Album module
];

/*========================================================*/
change your config/autoload/global.php according to below files

<?php
/**
 * Global Configuration Override
 *
 * You can use this file for overriding configuration values from modules, etc.
 * You would place values in here that are agnostic to the environment and not
 * sensitive to security.
 *
 * @NOTE: In practice, this file will typically be INCLUDED in your source
 * control, so do not include passwords or other sensitive information in this
 * file.
 */

return [
    'service_manager' => [
        'factories' => [
            \Zend\Db\Adapter\Adapter::class => \Zend\Db\Adapter\AdapterServiceFactory::class,
        ],
        // to allow other adapter to be called by
        
        // $sm->get('db1') or $sm->get('db2') based on the adapters config.
        
        'abstract_factories' => [
            'Zend\Db\Adapter\AdapterAbstractServiceFactory',
        ],
    ],
    
    
    'db' => [
        'driver'    => 'Pdo',
        'dsn'       => 'mysql:dbname=zf2_db;host=localhost;charset=utf8;',
        'username'  => 'root',

        'password'  => '',

        'adapters' => [
            'db2' => [
                'driver'    => 'Pdo',
                'dsn'       => 'mysql:dbname=zf3_db;host=localhost;charset=utf8;',
                'username'  => 'root',
                'password'  => '',
                PDO::ATTR_EMULATE_PREPARES => false
            ],
            'db3' => [
                'driver'    => 'Pdo',
                'dsn'       => 'mysql:dbname=db3;host=localhost;charset=utf8;',
                'username'  => 'foo',
                'password'  => 'bar',
                PDO::ATTR_EMULATE_PREPARES => false
            ]
        ],
    ],



];

 ?>  

Database Setup

Import zf3_db.sql into your database
Usage

and execute your new Album module at Browser

your-domain-name/album
your-domain-name/album/add
