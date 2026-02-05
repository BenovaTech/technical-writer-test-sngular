# Add a product creation endpoint (POST /products)

## Introduction

In this codelab, you will extend an existing Spring Boot REST API by adding a `POST /products` endpoint. The goal is to allow clients to create new products while keeping the API contract clean and maintainable.

You will:
- Introduce a request DTO to handle input data
- Implement product creation logic in the service layer
- Expose a new REST endpoint in the controller

By the end of this codelab, your implementation will match the `solution` branch.

---

## Step 1: Introduce a request DTO for product creation

### Goal

Create a dedicated request object to represent the data required to create a product. This avoids exposing the internal domain model directly and keeps the API contract explicit.

### What to do

Create a new class named `CreateProductRequest` under:
```
code/src/main/java/com/example/codelab/dto/
```

Add the fields needed to create a product, such as name and price, with proper validation annotations.
```java

public class CreateProductRequest {

    @NotBlank(message = "Product name is required")
    private String name;

    @NotNull(message = "Price is required")
    @Positive(message = "Price must be positive")
    private BigDecimal price;

}
```

### Expected outcome

The API can now accept structured and validated input data for product creation using a dedicated request object.
The request DTO intentionally contains only a subset of the Product fields, as some attributes (such as id or stock) are managed internally.

---

## Step 2: Add product creation logic to the service layer

### Goal

Encapsulate product creation logic in the service layer to keep the controller focused on request handling.

### What to do

Update the service class located at:
```
code/src/main/java/com/example/codelab/service/ProductService.java
```

Add a method that accepts a `CreateProductRequest`, creates a new `Product`, and persists it using the repository.
```java

import com.example.codelab.dto.CreateProductRequest;
import com.example.codelab.model.Product;
import com.example.codelab.repository.ProductRepository;
import org.springframework.stereotype.Service;

@Service
public class ProductService {

    private final ProductRepository productRepository;

    public ProductService(ProductRepository productRepository) {
        this.productRepository = productRepository;
    }

    public Product createProduct(CreateProductRequest request) {
        Product product = new Product();
        product.setName(request.getName());
        product.setPrice(request.getPrice());
        
        return productRepository.save(product);
    }
}
```

### Expected outcome

The service layer provides a clear and reusable entry point for creating products.

---

## Step 3: Expose the POST /products endpoint

### Goal

Expose an endpoint that allows clients to create new products with the correct HTTP status code and response.

### What to do

Update the controller located at:
```
code/src/main/java/com/example/codelab/controller/ProductController.java
```

Add a `POST /products` endpoint that accepts a validated `CreateProductRequest` and delegates creation to the service layer. The endpoint returns `201 Created` with a `Location` header.
```java

import com.example.codelab.dto.CreateProductRequest;
import com.example.codelab.model.Product;
import com.example.codelab.service.ProductService;
import jakarta.validation.Valid;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.*;

import java.net.URI;

@RestController
@RequestMapping("/products")
public class ProductController {

    private final ProductService productService;

    public ProductController(ProductService productService) {
        this.productService = productService;
    }

    @PostMapping
    public ResponseEntity<Product> createProduct(@Valid @RequestBody CreateProductRequest request) {
        return ResponseEntity.ok(productService.createProduct(request));
    }
}
```

### Expected outcome

Clients can create new products by sending a POST request to `/products`. The API returns the created product in the response body.

---
