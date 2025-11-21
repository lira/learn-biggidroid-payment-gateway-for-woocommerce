# BiggiDroid Payment Gateway for WooCommerce

A WordPress plugin that adds a "BiggiDroid Payment" gateway to WooCommerce. It integrates with WooCommerce (including WooCommerce Blocks) and provides admin settings for test/live mode and API keys. The project also includes a small JavaScript build setup using @wordpress/scripts for the checkout/block UI.

Note: Some details are not present in the repository. Where information is missing, TODO notes are included for maintainers to fill in.

## Information

This content are part of a Udemy Course, made for Adeleye Ayodeji.

Link to the course: https://www.udemy.com/share/10cIo73@HT-phJoiKzLV_5LQjzTLjaPj4jLPOL0lpXLCdXnm_ZFnYZ9CvEp2jydl_u5ZJdE=/

Personal page of Adeleye Ayodeji: https://www.udemy.com/user/adeleye-ayodeji/

## Table of Contents
- [Overview](#overview)
- [Stack](#stack)
- [Requirements](#requirements)
- [Installation](#installation)
- [Configuration](#configuration)
- [Build and Scripts](#build-and-scripts)
- [Environment and Configuration Variables](#environment-and-configuration-variables)
- [How to Run (Development)](#how-to-run-development)
- [Tests](#tests)
- [Project Structure](#project-structure)
- [Deployment](#deployment)
- [License](#license)
- [Changelog](#changelog)
- [Maintainers / Support](#maintainers--support)

## Overview
- Adds a custom payment gateway class that extends WooCommerce's credit card gateway API.
- Provides admin settings (enable/disable, title/description, test mode, test/live public/secret keys, etc.).
- Enqueues admin and checkout scripts.
- Registers WooCommerce Blocks payment method integration when Blocks are available.

Key files:
- Plugin entry point: biggidroid-payment.php
- Gateway implementation: includes/main-file.php (class Biggi_Droid_Payment_Gateway)
- Blocks support: includes/class-biggidroid-block-payment-method.php
- Admin JS: assets/js/admin.js
- Checkout JS: assets/js/checkout.js
- Block source: src/block.js (bundled to assets/js/block via @wordpress/scripts)


## Stack
- Language: PHP (WordPress plugin), JavaScript (build assets for admin/checkout/blocks)
- Platform: WordPress + WooCommerce
- Build tooling: Node.js with @wordpress/scripts
- Package manager: npm (package.json present)


## Requirements
- WordPress: TODO: document minimum supported version (e.g., 5.x+)
- WooCommerce: TODO: document minimum supported version (e.g., 7.x+)
- PHP: TODO: document minimum supported PHP version (e.g., 7.4+ or 8.0+)
- Node.js: for building assets, Node 18+ is recommended (compatible with @wordpress/scripts 26.x)

Additionally:
- WooCommerce must be active; otherwise the plugin shows an admin notice and does not initialize.


## Installation
1. Download or clone this repository into your WordPress installation under wp-content/plugins/learn-biggidroid-payment-gateway (folder name can vary).
2. Optional: Build the block assets (see Build and Scripts below). Prebuilt assets may already exist in assets/.
3. In WordPress Admin, go to Plugins and activate "BiggiDroid Payment Gateway".
4. Go to WooCommerce → Settings → Payments → BiggiDroid Payment and configure the gateway.


## Configuration
In WooCommerce payment settings for BiggiDroid Payment:
- Enable/Disable: Turn the gateway on or off.
- Title/Description: What customers see at checkout.
- Test Mode: Toggle between test and live environments.
- API Keys:
  - When Test Mode is enabled: set Test Public Key and Test Secret Key.
  - When Test Mode is disabled: set Live Public Key and Live Secret Key.

Admin UI behavior:
- assets/js/admin.js toggles visibility of the relevant key fields when you switch Test Mode.

Checkout:
- assets/js/checkout.js is enqueued on checkout to handle any front-end interactions required by the gateway.

Blocks support:
- If WooCommerce Blocks are available, the plugin registers a block payment method integration via includes/class-biggidroid-block-payment-method.php.

Webhook/Callback:
- The gateway includes a callback handler method (biggidroid_payment_callback in includes/main-file.php). This is typically used by payment providers to confirm transaction status.
- TODO: Document the exact callback/webhook URL that should be configured on the payment provider dashboard.
- TODO: Document the expected request parameters and signature/verification process, if applicable.

Payment Provider:
- The repository and code reference "BiggiDroid Payment". The package.json description mentions Monnify.
- TODO: Clarify whether the payment processor is BiggiDroid’s own service, Monnify, or an integration with Monnify via BiggiDroid. Update this README accordingly.


## Build and Scripts
This project uses @wordpress/scripts to build the block script from src/block.js into assets/js/block.

From the project root:
- Install dependencies:
  npm install

- Start development build with watch:
  npm run start

- Production build:
  npm run build

- Linting and formatting:
  npm run lint:js
  npm run lint:css
  npm run format

- Additional maintenance scripts (from package.json):
  - npm run check-engines
  - npm run check-licenses
  - npm run lint:md:docs
  - npm run lint:pkg-json
  - npm run packages-update
  - npm run plugin-zip (creates a distributable zip using @wordpress/scripts)

Scripts as defined in package.json:
- build: wp-scripts build src/block.js --output-path=assets/js/block
- start: wp-scripts start src/block.js --output-path=assets/js/block --watch
- plugin-zip: wp-scripts plugin-zip
- plus various lint/check commands via wp-scripts


## Environment and Configuration Variables
There are no .env files in this repository. All sensitive configuration is handled in WordPress Admin under the gateway settings:
- Test Mode: yes/no
- Test Public Key, Test Secret Key
- Live Public Key, Live Secret Key

Constants defined at runtime (see biggidroid-payment.php):
- BIGGI_DROID_PAYMENT_VERSION (uses time() for cache-busting assets)
- BIGGI_DROID_PAYMENT_PLUGIN_URL
- BIGGI_DROID_PAYMENT_PLUGIN_PATH
- BIGGIDROID_TEXT_DOMAIN

TODOs:
- If any site-level constants or filters must be set (e.g., via wp-config.php), document them here.


## How to Run (Development)
- Have a local WordPress environment with WooCommerce installed and activated.
- Place this plugin in wp-content/plugins and activate it.
- Run npm install, then npm run start to build and watch block assets while developing src/block.js.
- Make changes to PHP files as needed; they are loaded by WordPress directly.


## Tests
No tests are included in this repository at the moment.
- TODO: Add unit tests (PHPUnit) for gateway logic and webhook handling.
- TODO: Add JavaScript tests if block/frontend logic grows (Jest via @wordpress/scripts/jest-preset).


## Project Structure
- biggidroid-payment.php — Main plugin file; defines constants, hooks, and registers the gateway and Blocks integration.
- includes/
  - main-file.php — Contains the Biggi_Droid_Payment_Gateway class and core logic (settings, scripts, processing, callback handler).
  - class-biggidroid-block-payment-method.php — WooCommerce Blocks integration class.
- assets/
  - js/
    - admin.js — Toggles key fields visibility in admin based on Test Mode.
    - checkout.js — Front-end checkout behavior for the gateway.
    - block/ — Build output directory for the block bundle (generated by @wordpress/scripts).
- src/
  - block.js — Block source file (entry point for builds).
- templates/
  - admin_notice.php — Admin notice shown when WooCommerce is not active.
- package.json — NPM scripts and dependencies for building assets.
- package-lock.json — NPM lockfile.
- node_modules/ — Installed JS dependencies.


## Deployment
- Use npm run plugin-zip to generate a distributable zip archive of the plugin.
- Alternatively, zip the plugin folder (ensuring built assets are included) and install via WordPress Plugins → Add New → Upload Plugin.


## License
This plugin is licensed under the GPL-2.0-or-later license, as declared in package.json and biggidroid-payment.php.


## Changelog
- 0.1.0 — Initial public version (as per plugin header).


## Maintainers / Support
- Author: Adeleye Ayodeji
- TODO: Add support contact, issue tracker URL, and contribution guidelines if available.
