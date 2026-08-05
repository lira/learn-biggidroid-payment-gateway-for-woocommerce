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