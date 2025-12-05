# 🚀 Laravel 11 AJAX CRUD Using Yajra DataTables  
A modern and interactive CRUD system built using **Laravel 11**, **AJAX**, **Bootstrap 5**, and **Yajra DataTables** — with full create, read, update, delete operations performed **without page reload**.

---

# 🎯 Features

- ⚡ AJAX-based Create, Read, Update & Delete  
- 📊 Yajra DataTables (Server-side processing)  
- 🎨 Bootstrap 5 UI  
- 🧩 Modal-based forms   
- 🔄 RESTful Laravel Controller  
- 🔐 Laravel validation  
- 💾 MySQL / SQLite compatible  
- 🚀 Super-fast interactions (no page reload)

---

# 📁 Project Folder Structure

```
CRUD_USING_AJAX_DATATABLES/
├── app
│   ├── Http
│   │   ├── Controllers
│   │   │   ├── Controller.php
│   │   │   └── ProductController.php
│   ├── Models
│   │   ├── Product.php
│   │   └── User.php
│   └── Providers
│
├── bootstrap
├── config
│
├── database
│   ├── factories
│   ├── migrations
│   │   ├── 0001_01_01_000000_create_users_table.php
│   │   ├── 0001_01_01_000001_create_cache_table.php
│   │   ├── 0001_01_01_000002_create_jobs_table.php
│   │   └── 2025_12_04_083045_create_products_table.php
│   ├── seeders
│   └── database.sqlite
│
├── public
│   ├── css/
│   ├── js/
│   └── index.php
│
├── resources
│   ├── css
│   ├── js
│   └── views
│       ├── products.blade.php
│       └── welcome.blade.php
│
├── routes
│   ├── web.php
│   └── console.php
│
├── storage
├── tests
├── vendor
│
├── .env
├── artisan
├── composer.json
└── package.json
```

---

# 📚 Table of Contents

- [Features](#-features)  
- [Project Folder Structure](#-project-folder-structure)  
- [Installation](#-installation)  
- [Environment Setup](#-environment-setup)  
- [Migration](#-migration)  
- [Routes](#-routes)  
- [Controller](#-controller)  
- [Model](#-model)  
- [Blade View](#-blade-view)  
- [Run Application](#-run-application)

---

# ⚙️ Installation

```bash
composer create-project laravel/laravel TestAjax "11.*"
```

Install Yajra DataTables:

```bash
composer require yajra/laravel-datatables-oracle
```

---

# 🔧 Environment Setup

Update `.env`:

```env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=testajax
DB_USERNAME=root
DB_PASSWORD=
```

---

# 🗄️ Migration

Create migration:

```bash
php artisan make:migration create_products_table --create=products
```

Migration file:

```php
Schema::create('products', function (Blueprint $table) {
    $table->id();
    $table->string('name');
    $table->text('detail');
    $table->timestamps();
});
```

Run migration:

```bash
php artisan migrate
```

---

# 🛣️ Routes

In `routes/web.php`:

```php
use App\Http\Controllers\ProductController;

Route::resource('products', ProductController::class);
```

---

# 🎮 Controller

A complete AJAX-compatible CRUD controller using Yajra DataTables.

```php
public function index(Request $request)
{
    if ($request->ajax()) {
        $data = Product::query();

        return DataTables::of($data)
            ->addIndexColumn()
            ->addColumn('action', function($row){
                return '
                    <a href="#" data-id="'.$row->id.'" class="btn btn-info btn-sm showProduct">View</a>
                    <a href="#" data-id="'.$row->id.'" class="btn btn-primary btn-sm editProduct">Edit</a>
                    <a href="#" data-id="'.$row->id.'" class="btn btn-danger btn-sm deleteProduct">Delete</a>
                ';
            })
            ->rawColumns(['action'])
            ->make(true);
    }

    return view('products');
}
```

---

# 🧬 Model

`app/Models/Product.php`

```php
class Product extends Model
{
    protected $fillable = ['name', 'detail'];
}
```

---

# 🖼️ Blade View

`resources/views/products.blade.php`  
Contains:  
✔ DataTable  
✔ AJAX modals  
✔ Create/Edit forms  
✔ Delete confirmation  
✔ jQuery scripts  

*(Full blade code already included earlier.)*

---

# ▶️ Run Application

```bash
php artisan serve
```

Open in browser:

```
http://localhost:8000/products
```

---

# 🎉 Done!

Your **Laravel 11 AJAX CRUD** system is ready — clean, fast, and fully interactive.


<img width="975" height="363" alt="image" src="https://github.com/user-attachments/assets/2143b369-e9bf-4480-9686-f81bf6e0fede" />


<img width="975" height="391" alt="image" src="https://github.com/user-attachments/assets/42dd0fa7-7630-4cd0-8dec-e091942cf19b" />


<img width="975" height="373" alt="image" src="https://github.com/user-attachments/assets/ee1e9950-05f6-40ff-8cc9-eee60c1a564e" />


