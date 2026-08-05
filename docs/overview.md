## Overview

- Adds a custom payment gateway class that extends WooCommerce's credit card gateway API.
- Provides admin settings (enable/disable, title/description, test mode, test/live public/secret keys, etc.).
- Enqueues admin and checkout scripts.
- Registers WooCommerce Blocks payment method integration when Blocks are available.

Key files:
- Plugin entry point: `biggidroid-payment.php`
- Gateway implementation: `includes/main-file.php` (class `Biggi_Droid_Payment_Gateway`)
- Blocks support: `includes/class-biggidroid-block-payment-method.php`
- Admin JS: `assets/js/admin.js`
- Checkout JS: `assets/js/checkout.js`
- Block source: `src/block.js` (bundled to `assets/js/block` via `@wordpress/scripts`)