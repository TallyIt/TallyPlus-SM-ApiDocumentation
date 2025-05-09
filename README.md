# Tally+ Small Market OpenAPI Documentation
This repository includes Swagger UI to enable rendering OpenAPI documentation.

## Maintaining OpenAPI Documentation
The API documentation is contained in `.\OpenAPI\tallyplus-sm-openapi.yaml` using the OpenAPI 3.0.1 standard.

## Swagger UI
The main Swagger UI page is `.\index.html`.

The majority of Swagger UI components are inside the `.\dist\` directory with only `.\index.html` and `.\swagger-ui.version` in root.

## Extending
The current needs are simple, so the repository structure is simple.

This repository can be extended to handle increased complexity.

**Adding OpenAPI Files**
The script that loads the OpenAPI YAML files for Swagger UI is `.\dist\swagger-initializer.js` which is currently only loads the one file.

As API documentation complexity grows, the API definitions can be encapsulated into multiple files, and `.\dist\swagger-initializer.js` can be updated similar to the below to support multiple files. Each file will have its own page and be selectable from a drop-down within the Swagger UI.

``` javascript
window.onload = function() {
  //<editor-fold desc="Changeable Configuration Block">

  window.ui = SwaggerUIBundle({
    urls: [
      // Category A
      { url: "./OpenAPI/CategoryA/file1.yaml", name: "Category A - 1" },
      { url: "./OpenAPI/CategoryA/file2.yaml", name: "Category A - 2" },
      
      // Category B
      { url: "./OpenAPI/CategoryB/file001.yaml", name: "Category B - 001" },
      { url: "./OpenAPI/CategoryB/file002.yaml", name: "Category B - 002" },
      
      // ...
    ],
    // Enable tag sorting for better organization within each spec
    tagsSorter: 'alpha',
    // Enable operation sorting
    operationsSorter: 'alpha',
    dom_id: '#swagger-ui',
    deepLinking: true,
    presets: [
      SwaggerUIBundle.presets.apis,
      SwaggerUIStandalonePreset
    ],
    plugins: [
      SwaggerUIBundle.plugins.DownloadUrl
    ],
    layout: "StandaloneLayout"
  });

  //</editor-fold>
};
```