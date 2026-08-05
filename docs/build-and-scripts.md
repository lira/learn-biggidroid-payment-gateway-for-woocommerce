## Build and Scripts

This project uses @wordpress/scripts to build the block script from src/block.js into assets/js/block.

From the project root:
- Install dependencies:
  ```
  npm install
  ```

- Start development build with watch:
  ```
  npm run start
  ```

- Production build:
  ```
  npm run build
  ```

- Linting and formatting:
  ```
  npm run lint:js
  npm run lint:css
  npm run format
  ```

- Additional maintenance scripts (from package.json):
  ```
  npm run check-engines
  npm run check-licenses
  npm run lint:md:docs
  npm run lint:pkg-json
  npm run packages-update
  npm run plugin-zip (creates a distributable zip using @wordpress/scripts)
  ```

Scripts as defined in package.json:
- build: wp-scripts build src/block.js --output-path=assets/js/block
- start: wp-scripts start src/block.js --output-path=assets/js/block --watch
- plugin-zip: wp-scripts plugin-zip
- plus various lint/check commands via wp-scripts