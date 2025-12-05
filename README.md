🚀 Laravel 11 AJAX CRUD Using Yajra DataTables

A complete step-by-step guide to building modern CRUD without page reload.

This repository demonstrates how to create a full AJAX-based CRUD system in Laravel 11, using:

✔️ Yajra DataTables
✔️ Bootstrap 5
✔️ jQuery AJAX
✔️ Modal-based Create / Edit / View
✔️ RESTful Controller
✔️ No Page Reload CRUD

📌 Features

AJAX Create, Read, Update & Delete

Server-side DataTables

Bootstrap 5 UI

Clean modal-based interactions

Laravel 11 REST API structure

🛠️ Step 1: Install Laravel 11
composer create-project laravel/laravel TestAjax "11.*"

🛠️ Step 2: Install Yajra DataTables (Laravel 11 Compatible)
composer require yajra/laravel-datatables-oracle

🛠️ Step 3: Database Configuration

Update .env:

DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=testajax
DB_USERNAME=root
DB_PASSWORD=

🛠️ Step 4: Create Migration
php artisan make:migration create_products_table --create=products

Migration File (database/migrations/...create_products_table.php)
<?php

use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

return new class extends Migration
{
    public function up(): void
    {
        Schema::create('products', function (Blueprint $table) {
            $table->id();
            $table->string('name');
            $table->text('detail');
            $table->timestamps();
        });
    }

    public function down(): void
    {
        Schema::dropIfExists('products');
    }
};


Run migration:

php artisan migrate

🛠️ Step 5: Create Route

Add inside routes/web.php:

use App\Http\Controllers\ProductController;

Route::resource('products', ProductController::class);

🛠️ Step 6: Controller & Model
ProductController.php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;
use App\Models\Product;
use Yajra\DataTables\Facades\DataTables;
use Illuminate\Http\JsonResponse;

class ProductController extends Controller
{
    public function index(Request $request)
    {
        if ($request->ajax()) {
            $data = Product::query();

            return DataTables::of($data)
                ->addIndexColumn()
                ->addColumn('action', function($row){
                    $btn = '<a href="javascript:void(0)" data-id="'.$row->id.'" class="btn btn-info btn-sm showProduct">View</a>';
                    $btn .= '<a href="javascript:void(0)" data-id="'.$row->id.'" class="btn btn-primary btn-sm editProduct">Edit</a>';
                    $btn .= '<a href="javascript:void(0)" data-id="'.$row->id.'" class="btn btn-danger btn-sm deleteProduct">Delete</a>';
                    return $btn;
                })
                ->rawColumns(['action'])
                ->make(true);
        }

        return view('products');
    }

    public function store(Request $request): JsonResponse
    {
        $request->validate([
            'name' => 'required',
            'detail' => 'required',
        ]);

        Product::updateOrCreate(
            ['id' => $request->product_id],
            ['name' => $request->name, 'detail' => $request->detail]
        );

        return response()->json(['success' => 'Product saved successfully.']);
    }

    public function show($id): JsonResponse
    {
        return response()->json(Product::find($id));
    }

    public function edit($id): JsonResponse
    {
        return response()->json(Product::find($id));
    }

    public function destroy($id): JsonResponse
    {
        Product::find($id)->delete();
        return response()->json(['success' => 'Product deleted successfully.']);
    }
}

🛠️ Step 7: Product Model

app/Models/Product.php

<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Database\Eloquent\Model;

class Product extends Model
{
    use HasFactory;

    protected $fillable = [
        'name', 'detail'
    ];
}

🛠️ Step 8: Blade File

Create:
📁 resources/views/products.blade.php

<!DOCTYPE html>
<html>
<head>
    <title>Laravel 11 Ajax CRUD</title>
    <meta name="csrf-token" content="{{ csrf_token() }}">
    <link href="https://cdnjs.cloudflare.com/ajax/libs/twitter-bootstrap/5.0.1/css/bootstrap.min.css" rel="stylesheet">
    <link href="https://cdn.datatables.net/1.11.4/css/dataTables.bootstrap5.min.css" rel="stylesheet">
    <script src="https://code.jquery.com/jquery-3.5.1.js"></script>
    <script src="https://cdn.datatables.net/1.11.4/js/jquery.dataTables.min.js"></script>
    <script src="https://cdn.datatables.net/1.11.4/js/dataTables.bootstrap5.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/js/bootstrap.bundle.min.js"></script>
</head>
<body>
<div class="container">
    <div class="card mt-5 shadow">
        <h2 class="card-header">Laravel 11 Ajax CRUD</h2>

        <div class="card-body">

            <div class="text-end mb-3">
                <button class="btn btn-success btn-sm" id="createNewProduct">Create New Product</button>
            </div>

            <table class="table table-bordered data-table">
                <thead>
                    <tr>
                        <th>No</th>
                        <th>Name</th>
                        <th>Details</th>
                        <th width="280px">Action</th>
                    </tr>
                </thead>
                <tbody></tbody>
            </table>

        </div>
    </div>
</div>

<!-- Modals (Create/Edit/View) -->
<!-- ... full modal + JS included ... -->


(I can include full HTML & JS again if needed.)

▶️ Run Laravel App
php artisan serve


Visit:

http://localhost:8000/products

📷 Preview
✔️ Product List Page
✔️ Create Product Modal
✔️ Edit Product Modal

(You can add your images here.)
