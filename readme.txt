UPS XML Rates v1.7.7 for Zen Cart (for Zen Cart versions 1.5.3 and later)

Original Copyright (c) 2003 Torin Walker, torinwalker@rogers.com
Insurance Support 2005 Joe McFrederick, jomcfred@oldeparsonage.com
Modified for zen-cart 1.2.5d by Dennis Sayer - July 9, 2005, 
                                dennis.s.sayer@brandnamebatteries.com
Updated for zen-cart 1.5.1 by Brian Gundlach - June 10, 2014,
                              Brian@gundlach-marketing.com

===============================================================================
  This program is free software; you can redistribute it and/or modify it under
the terms of the GNU General Public License as published by the Free Software 
Foundation; either version 2 of the License, or (at your option) any later version.

  This program is distributed in the hope that it will be useful, but WITHOUT 
ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS 
FOR A PARTICULAR PURPOSE. See the GNU General Public License for more details.

You should have received a copy of the GNU General Public License along with 
this program. If not, you may obtain one by writing to and requesting one from

	The Free Software Foundation, Inc.,
        59 Temple Place, Suite 330,
        Boston, MA 02111-1307 USA
===============================================================================

Updated/modified/repackaged for osCommerce 2.2 MS2 by Stuart Owens 11/14/04
Time in Transit fixed by Greg MacLellan 11/15/04
A few bugfixes and installation added to upsxml.php JanZ 11/27/04 (1.1.3)
Bugfix for ship in cart: Jackie Edwards (1.1.3a)
More options for cURL (CLI support added and logging of cURL errors) JanZ 12/18/04 (1.1.4)
Updated/modified/repackaged for zen-cart 1.2.5d by Dennis Sayer 07/09/2005

Thanks to the many other authors who laid down their efforts in contributions 
from which has produced this. Your efforts are greatly appreciated.

Credits:
    Original Contribution and updates - Torin Walker
    Time In Transit capability - Donna Gordon
    Bug fixes - Fox Morrey
    Admin selectable methods and bug fixes - Jan Zonjee/Stuart Owens
    Modifyed for zen-cart 1.2.5d by Dennis Sayer
    Tested for zen-cart 1.3+ by Dennis Sayer
    V1.5 testing, bugfixes, & installation update - Brian Gundlach
	small fix for zen cart 1.5.5x and future PHP compatibility - lankeeyankee

===============================================================================
A note from Dennis Sayer 
-----------------------------------
  Thank you to Torin Walker for giving this code a GNU General Public License. 
I have removed your comments to web sites that no longer exist. I have also
changed or deleted text that is not related to zen-cart.

===============================================================================
Description
-------------------
  This module provides the eCommerce zen-cart community with the long-awaited
XML version of the UPS Rates and Services gatway. It supports mutliple 
(customer facing) languages, multiple geographic origins, and implements the 
most necessary features offered by the UPS Rates and Services system. The 
module connects to UPS and retrieves a list of available shipping methods and 
prices and presents them to the user.

Settings are changed in the admin interface under
        Admin->Modules->Shipping->United Parcel Service (upsxml)

        - Packaging Not supported for zen-cart as of July 9 2005 (DSS)
        Admin->Tools->Packaging (if dimensional support is enabled)
        - Packaging Not supported for zen-cart as of July 9 2005 (DSS)

The administrative interface shows shipper (not customer) related variables 
such as package type and origin in English, but customer-facing product names
(the name UPS uses to describe its services, such as 'Express Plus', and 
'Next Day A.M.' can be multi-lingual.

-- Torin Walker

===============================================================================
INSTALLATION
===============================================================================

--------
STEP 1
--------
BACKUP your database and all files that that are related to your store.

--------
STEP 2
--------
Change any folder names in the UPSXML zip extraction to meet the folder structure on your site. 
The "catalog" folder below would match to the folder where your site is installed.
The files needed are:
  catalog/includes/classes/xmldocument.php
  catalog/includes/languages/english/modules/shipping/upsxml.php
  catalog/includes/modules/shipping/upsxml.php
  catalog/includes/templates/template_default/images/icons/shipping_ups.gif
  catalog/logs/upsxml.log

--------
STEP 3
--------
If you have all three of these:
  UPS Rates account username
  UPS Rates account password
  UPS Rates Access Key 
then goto STEP 4.
1) Register at UPS for an account. 
   https://www.ups.com/one-to-one/register?appid=sso&sysid=myups
2) Goto Business Technology Solutions
   https://www.ups.com/upsdeveloperkit/manageaccesskeys
3) Click on 'Request New Access Key'
   or go to https://www.ups.com/upsdeveloperkit/requestaccesskey
   Fill in any requested information
4) Click on 'Request Access Key'
5) Follow the UPS web sites instructions to Get a License
6) Write down your XML Access Key. You will need to enter it into the UPSXML module settings.

--------
STEP 4
--------
In admin, choose Modules->Shipping, and activate the new United Parcel Service (upsxml) module.
Edit the module and set your service options:

        UPS Rates Access Key (obtain from UPS)
        UPS Rates account username (obtain from UPS)
        UPS Rates account password (obtain from UPS)
        Pickup method
        Packaging Type
        Customer Classification Code
        Shipping Origin (determines what products names are shown based on origin)
        Origin City (required for some countries)
        Origin State/Province (two letter ISO 3166 code)
        Origin Country (two letter ISO 3166 code)
        Origin Zip/Postal Code
        Test or Production mode
        Unit Weight
        Unit Length
        Quote Type
        Handling Fee
        Tax Class
        Shipping Zone
        Sort Order
        Shipping Methods
        Shipping Delay

If you have any questions regarding the above settings, please refer to the 
documentation provided to you by UPS when you signed up for and received your 
access key. 

--------
STEP 5
--------
Test by setting your customer destination to all sorts of different places, and
running through the shipping process several times. Please test thoroughly 
before committing to its use.

If you fail to get quotes, an error message will usually tell you why. Make 
sure your origin information is correct, and use the proper two-letter codes 
for your country and state/province.

If you STILL don't get any quotes, you can enable logging which will record the
request/response of the transactions and any cURL errors. Starting with v1.7,
just update the shipping method's debug via your admin's Modules->Shipping, editing
the upsxml module.


===============================================================================

--------------
1.5 Changelog
--------------

- Updated Mexico Origin module names in language file
- included a logfile & logfile path, settings
- changed appropriate ups urls in install

1.5.1 Changes
-------------
- updated CURL implementation
- fixed PHP compatibility issues with PHP 5.3 and newer
- changed suggested logfile location to /logs/ folder
- removed the need to duplicate the xmldocument.php into the admin folder
- added Customer Classification Code 00 to get account rates (requires that you actually have negotiated rates)
- Compatible with Zen Cart 1.5.1, 1.5.2, 1.5.3, 1.5.4, 1.5.5

1.6.1 simply changed mysql_ function to mysqli_ for zen cart 1.5.5 and future PHP compatibility

-------------
1.7 Changelog (lat9)
-------------

- Updated /includes/classes/xmldocument.php for PHP 7.0+ interoperability.
- Added a "Shipper Number" field to the configuration.  This value is needed if your store
    wants to receive your UPS-negotiated rates.
- Added configuration settings, allowing you to control whether or not the weight and/or
    transit-time displays should be included.
- Added a configuration setting to allow you to control whether or not the plugin's debug
    output is to be activated.
- Updated the plugin's "title", displaying the current version only during admin configuration.

-------------
1.7.1 Changelog (lat9)
-------------

- An invalid "Currency Code" resulted in invalid results returned when negotiated rates were enabled.
  - Updated /includes/classes/xmldocument.php, /includes/languages/english/modules/shipping/upsxml.php,
    and /includes/modules/shipping/upsxml.php.
    
-------------
1.7.2 Changelog (lat9)
-------------

- Don't issue the invalid "Currency Code" message until the module is installed and enabled.
- Don't request negotiated rates if the ship-to state has not been set (i.e. when used by the shipping-estimator).
  - Updated /includes/modules/shipping/upsxml.php
    
-------------
1.7.3 Changelog (lat9, benharold)
-------------

- Correct undefined constants' issues (required for PHP 7.2+)
- Updated the shipping method's debug log filename to include the date on which the log was made.
- Don't return methods if an error is reported by UPS.
- Remove support for Zen Carts prior to 1.5.3.
  - Updated 
    1. /includes/classes/xmldocument.php
    2. /includes/languages/english/modules/shipping/upsxml.php
    3. /includes/modules/shipping/upsxml.php
    
-------------
1.7.4 Changelog (lat9)
-------------

- Remove unwanted directory-separator from UPS icon
- Remove single-quotes from numeric fields inserted on shipping-method installation.
  - Updated /includes/modules/shipping/upsxml.php
  
-------------
1.7.5 Changelog (lat9)
-------------

- Correctly use UPS-supplied messages, if present, on a quote error
- Restore 'MODULE_SHIPPING_UPSXML_RATES_ORIGIN' setting, "lost" in v1.7.4.
  - Updated /includes/modules/shipping/upsxml.php
  
-------------
1.7.6 Changelog (lat9)
-------------

- Correct insurance not recognized when using the shipping estimator.
  - Updated /includes/modules/shipping/upsxml.php
  
-------------
1.7.7 Changelog (lat9)
-------------

- Correct PHP notice when viewing in admin's "Modules->Shipping"
- Display "New version available" information **only** when viewing the admin's "Modules->Shipping"
- Correctly offer "Next Day Air Early", if configured and provided in the UPS quote.
  - Updated /includes/modules/shipping/upsxml.php

