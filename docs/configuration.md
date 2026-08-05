## Configuration

In WooCommerce payment settings for BiggiDroid Payment:
- Enable/Disable: Turn the gateway on or off.
- Title/Description: What customers see at checkout.
- Test Mode: Toggle between test and live environments.
- API Keys:
  - When Test Mode is enabled: set Test Public Key and Test Secret Key.
  - When Test Mode is disabled: set Live Public Key and Live Secret Key.

Admin UI behavior:
- `assets/js/admin.js` toggles visibility of the relevant key fields when you switch Test Mode.

Checkout:
- `assets/js/checkout.js` is enqueued on checkout to handle any front-end interactions required by the gateway.

Blocks support:
- If WooCommerce Blocks are available, the plugin registers a block payment method integration via `includes/class-biggidroid-block-payment-method.php`.

Webhook/Callback:
- The gateway includes a callback handler method (`biggidroid_payment_callback` in `includes/main-file.php`). This is typically used by payment providers to confirm transaction status.
- TODO: Document the exact callback/webhook URL that should be configured on the payment provider dashboard.
- TODO: Document the expected request parameters and signature/verification process, if applicable.

Payment Provider:
- The repository and code reference "BiggiDroid Payment". The package.json description mentions Monnify.
- TODO: Clarify whether the payment processor is BiggiDroid’s own service, Monnify, or an integration with Monnify via BiggiDroid. Update this README accordingly.