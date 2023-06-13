# Pemrograman Web 02 - Pertemuan 13
## Upload File Gambar
### Langkah-langkah Praktikum

#### Upload Gambar pada Artikel
Menambahkan fungsi unggah gambar pada tambah artikel.
Buka kembali Controller Artikel pada project sebelumnya, sesuaikan kode pada method
add seperti berikut:

```php
public function add()
{
// validasi data.
$validation = \Config\Services::validation();
$validation->setRules(['judul' => 'required']);
$isDataValid = $validation->withRequest($this->request)->run();
if ($isDataValid)
{
$file = $this->request->getFile('gambar');
$file->move(ROOTPATH . 'public/gambar');
$artikel = new ArtikelModel();
$artikel->insert([
'judul' => $this->request->getPost('judul'),
'isi' => $this->request->getPost('isi'),
'slug' => url_title($this->request->getPost('judul')),
'gambar' => $file->getName(),
]);
return redirect('admin/artikel');
}
$title = "Tambah Artikel";
return view('artikel/form_add', compact('title'));
}
```

Kemudian pada file views/artikel/form_add.php tambahkan field input file seperti
berikut.

```html
<p>
<input type="file" name="gambar">
</p>
```

Dan sesuaikan tag form dengan menambahkan ecrypt type seperti berikut.

```html
<form action="" method="post" enctype="multipart/form-data">
```

Ujicoba file upload dengan mengakses menu tambah artikel.

![Screenshot (115)](https://github.com/SatrioPratama75/PW02-13/assets/92651803/3077228e-fc94-4461-9d21-2b95b4f20308)

# Sekian Terima kasih
