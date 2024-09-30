<p align="center"><a href="https://laravel.com" target="_blank"><img src="https://raw.githubusercontent.com/laravel/art/master/logo-lockup/5%20SVG/2%20CMYK/1%20Full%20Color/laravel-logolockup-cmyk-red.svg" width="400" alt="Laravel Logo"></a></p>

# Laravel API Demo with Swagger Documentation

This is a demo repository showcasing a Laravel API with integrated Swagger documentation. The project uses the Laravel framework along with Swagger-php and L5-Swagger packages to generate and display API documentation via Swagger UI.

## Getting Started

### Prerequisites

Ensure you have the following installed before proceeding:
- PHP >= 8.0
- Composer
- Laravel >= 8.0
- A web server (Apache, Nginx, or Laravel's built-in server)

### Installation

1. **Clone the repository:**
   ```bash
   git clone <repo-url>
   ```

2. **Navigate to the project directory:**
   ```bash
   cd <your-repo-directory>
   ```

3. **Install Laravel and dependencies:**
   If Laravel is not already installed, install it using Composer:
   ```bash
   composer create-project --prefer-dist laravel/laravel .
   ```

4. **Install the necessary Composer packages:**
   ```bash
   composer require zircote/swagger-php
   composer require darkaonline/l5-swagger
   ```

5. **Publish the Swagger configuration:**
   ```bash
   php artisan vendor:publish --provider "L5Swagger\L5SwaggerServiceProvider"
   ```

### Usage

1. **Create the UsersController resource:**
   ```bash
   php artisan make:controller Api/UsersController -r
   ```

2. **Add API routes:**
   In `routes/api.php`, add the following route:
   ```php
   Route::resource('users', 'App\Http\Controllers\Api\UsersController');
   ```

3. **Add Swagger Annotations:**
   In `app/Http/Controllers/Api/Controller.php`, add the following PHPDoc comment:
   ```php
   /**
    * @OA\Info(title="My First API", version="0.1")
    */
   ```

   Then in `app/Http/Controllers/Api/UsersController.php`, document the `index` method as follows:
   ```php
   /**
    * @OA\Get(
    *     path="/api/users",
    *     @OA\Response(response="200", description="Display a listing of users.")
    * )
    */
   ```

4. **Generate Swagger documentation:**
   Run the following command to generate Swagger documentation:
   ```bash
   php artisan l5-swagger:generate
   ```

5. **Run the server:**
   Start the Laravel development server:
   ```bash
   php artisan serve
   ```

6. **Access Swagger UI:**
   Visit the following URL to access the Swagger UI and explore your API documentation:
   ```
   http://127.0.0.1:8000/api/documentation
   ```

### Available API Endpoints

The API exposes the following routes:

| Method | Endpoint         | Description                  |
|--------|------------------|------------------------------|
| GET    | `/api/users`      | Display a listing of users.  |
| POST   | `/api/users`      | Store a new user.            |
| GET    | `/api/users/{id}` | Display a specific user.     |
| PUT    | `/api/users/{id}` | Update a specific user.      |
| DELETE | `/api/users/{id}` | Delete a specific user.      |

### Swagger Annotations Example

You can document your API methods using Swagger annotations. Below is an example of how to document a `GET` request in `UsersController`:

```php
/**
 * @OA\Get(
 *     path="/api/users",
 *     summary="Get list of users",
 *     @OA\Response(
 *         response=200,
 *         description="A list of users."
 *     )
 * )
 */
public function index()
{
    // Your code to return a list of users
}
```

### Conclusion

This project integrates Laravel with Swagger to automatically generate and display API documentation. The Swagger UI can be used to test and explore your API easily.

For more information on the packages used in this project, check out the following documentation:
- [Laravel](https://laravel.com/docs)
- [Swagger-PHP](https://zircote.github.io/swagger-php/)
- [L5 Swagger](https://github.com/DarkaOnLine/L5-Swagger)
