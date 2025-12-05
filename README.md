
✨//Laravel Installation Code

⭐composer create-project laravel/laravel TestAjax "11.*"



✨Install Yajra Datatable (Correct package install.. (Laravel 11 compatible))

⭐composer require yajra/laravel-datatables-oracle


✨//Migration Code

⭐php artisan make:migration create_products_table --create=products

⭐ php artisan migrate



✨//Add This Code In Your Blade Code
<!-- DataTables CSS -->
    <link href="https://cdn.datatables.net/1.11.4/css/dataTables.bootstrap5.min.css" rel="stylesheet">


<!-- DataTables JS -->
    <script src="https://cdn.datatables.net/1.11.4/js/jquery.dataTables.min.js"></script>
    <script src="https://cdn.datatables.net/1.11.4/js/dataTables.bootstrap5.min.js"></script

            <!-- DataTable -->
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



✨//Initialize DataTable Code


    /*------------------------------------------
       Initialize DataTable
    -------------------------------------------*/
    var table = $('.data-table').DataTable({
        processing: true,
        serverSide: true,        // Server-side processing
        ajax: "{{ route('products.index') }}",  // Fetch data
        columns: [
            {data: 'id', name: 'id'},           // Product ID
            {data: 'name', name: 'name'},       // Product Name
            {data: 'detail', name: 'detail'},   // Product Detail
            {data: 'action', name: 'action', orderable: false, searchable: false}, // Action buttons
        ]
    });


OUTPUT:-


<img width="975" height="363" alt="image" src="https://github.com/user-attachments/assets/a53631d2-57e1-4913-94eb-a11a85b55758" />
<img width="975" height="391" alt="image" src="https://github.com/user-attachments/assets/89216a25-832a-4a87-913b-43137adaa5b2" />
<img width="975" height="373" alt="image" src="https://github.com/user-attachments/assets/0fb8b664-f4e1-4902-9df0-5a8d55970b68" />




