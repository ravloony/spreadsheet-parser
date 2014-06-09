Akeneo Spreadsheet Parser
=========================

This component is designed to extract data from spreadsheets, while being easy on resources, even for large files.

The actual version of the spreadsheet parser only works with xlsx files.

[![Scrutinizer Code Quality](https://scrutinizer-ci.com/g/akeneo/spreadsheet-parser/badges/quality-score.png?b=master)](https://scrutinizer-ci.com/g/akeneo/spreadsheet-parser/?branch=master)

Installing the package
----------------------

From your application root:

    $ php composer.phar require --prefer-dist "akeneo/spreadsheet-parser"


Usage
-----

To extract data from an XLSX spreadsheet, use the following code:

    <?php
    
    use Akeneo\Component\SpreadsheetParser\SpreadsheetParser;

    $workbook = SpreadsheetParser::open('myfile.xlsx');

    $myWorksheetIndex = $workbook->getWorksheetIndex('myworksheet');
    
    foreach ($workbook->createIterator($myWorksheetIndex) as $rowIndex => $values) {
        var_dump($rowIndex, $values);
    }


By using the CSV parser options, you can specify the format of your CSV file :

    <?php
    
    use Akeneo\Component\SpreadsheetParser\SpreadsheetParser;

    $workbook = SpreadsheetParser::open('myfile.csv');

    $iterator = $workbook->createIterator(
        0,
        [
            'encoding'  => 'UTF-8',
            'length'    => null,
            'delimiter' => ',',
            'enclosure' => '"',
            'escape'    => '\\'
        ]
    );
   
    
    foreach ($workbook->createIterator($myWorksheetIndex) as $rowIndex => $values) {
        var_dump($rowIndex, $values);
    }


Running the tests
-----------------

To run unit tests, use phpspec:

    $ php bin/phpspec run
    

To run integration tests, use phpunit:

    $ phpunit
    
    
