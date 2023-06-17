# ERD-karyawan

![image](https://github.com/verz666/karyawan/assets/115523263/ca9c533e-8b58-40e8-a246-fc39b618d1fd)

## table perusahaan 

    CREATE TABLE Company (
    id_p VARCHAR(3) PRIMARY KEY,
    nama VARCHAR(20),
    alamat VARCHAR(20)
    );

![image](https://github.com/verz666/karyawan/assets/115523263/ca28ba57-b58c-4811-b0e9-d374c3a375bf)

## table departemen

    CREATE TABLE Department (
    id_dept VARCHAR(3) PRIMARY KEY,
    nama VARCHAR(20),
    id_p VARCHAR(3),
    manajer_nik VARCHAR(3),
    FOREIGN KEY (id_p) REFERENCES Company (id_p),
    FOREIGN KEY (manajer_nik) REFERENCES Employee (nik)
    );

![image](https://github.com/verz666/karyawan/assets/115523263/c7b39f48-fac7-41d7-9718-1a9eb81683a4)

## table karyawan

    CREATE TABLE Employee (
    nik VARCHAR(3) PRIMARY KEY,
    nama VARCHAR(20),
    id_dept VARCHAR(3),
    sup_nik VARCHAR(3),
    FOREIGN KEY (id_dept) REFERENCES Department (id_dept),
    FOREIGN KEY (sup_nik) REFERENCES Employee (nik)
    );

![image](https://github.com/verz666/karyawan/assets/115523263/31f3b04a-c03c-4268-b3d4-e01427bfe4d0)

## table project

    CREATE TABLE Project (
    id_proj VARCHAR(4) PRIMARY KEY,
    nama VARCHAR(20),
    tgl_mulai DATE,
    tgl_selesai DATE,
    status INT
    );

![image](https://github.com/verz666/karyawan/assets/115523263/feacfce3-40e7-4f17-b3c2-1d16e515ce75)

## table project_detail

    CREATE TABLE Project_Employee (
    id_proj VARCHAR(4),
    nik VARCHAR(3),
    FOREIGN KEY (id_proj) REFERENCES Project (id_proj),
    FOREIGN KEY (nik) REFERENCES Employee (nik)
    );

![image](https://github.com/verz666/karyawan/assets/115523263/98b37503-ec30-48da-8604-a2501150d485)

## menampilkan nama manajer tiap departement 

    SELECT d.nama AS departemen, e.nama AS manajer
    FROM Department d
    LEFT JOIN Employee e ON d.manajer_nik = e.nik;

![image](https://github.com/verz666/karyawan/assets/115523263/2d43af8f-a9ff-411e-a36a-247610d4ce20)

## Menampilkan Nama Supervisor tiap karyawan

    SELECT e.nik, e.nama, d.nama AS departemen, s.nama AS supervisor
    FROM Employee e
    LEFT JOIN Department d ON e.id_dept = d.id_dept
    LEFT JOIN Employee s ON e.sup_nik = s.nik;

![image](https://github.com/verz666/karyawan/assets/115523263/630d763a-52c3-481d-a2f0-a43ac271e090)

## Menampilkan daftar karyawan yang bekerja pada project A

    SELECT e.nik, e.nama
    FROM Employee e
    JOIN Project_Employee pe ON e.nik = pe.nik
    JOIN Project p ON pe.id_proj = p.id_proj
    WHERE p.nama = 'A';

![image](https://github.com/verz666/karyawan/assets/115523263/4312cd0e-d9a0-4d17-9fc2-6a89477be5c2)

-----

# Latihan Praktikum

Buat query untuk menampilkan:
1. Departemen apa saja yang terlibat dalam tiap-tiap project
2. Jumlah karyawan tiap departemen yang bekerja pada tiap-tiap project
3. Ada berapa project yang sedang dikerjakan oleh departemen RnD? (ket: project berjalan adalah yang statusnya 1)
4. Berapa banyak project yang sedang dikerjakan oleh Ari?
5. Siapa saja yang mengerjakan projcet B?

----

## 1. Departemen apa saja yang terlibat dalam tiap-tiap project

    SELECT p.nama AS project, d.nama AS departemen
    FROM Project p
    INNER JOIN Project_Employee pe ON p.id_proj = pe.id_proj
    INNER JOIN Employee e ON pe.nik = e.nik
    INNER JOIN Department d ON e.id_dept = d.id_dept;

![image](https://github.com/verz666/karyawan/assets/115523263/2b62ff42-aaba-4d1c-aaa2-4e51bd14d00b)

## 2.  Jumlah karyawan tiap departemen yang bekerja pada tiap-tiap project

    SELECT p.nama AS project, d.nama AS departemen, COUNT(*) AS jumlah_karyawan
    FROM Project p
    INNER JOIN Project_Employee pe ON p.id_proj = pe.id_proj
    INNER JOIN Employee e ON pe.nik = e.nik
    INNER JOIN Department d ON e.id_dept = d.id_dept
    GROUP BY p.nama, d.nama;

![image](https://github.com/verz666/karyawan/assets/115523263/09d0cd6e-a8f4-4af8-bd69-d4377227c576)

## 3. Ada berapa project yang sedang dikerjakan oleh departemen RnD? (ket: project berjalan adalah yang statusnya 1)

    SELECT COUNT(*) AS jumlah_project
    FROM Project_Employee pe
    INNER JOIN Employee e ON pe.nik = e.nik
    INNER JOIN Department d ON e.id_dept = d.id_dept
    INNER JOIN Project p ON pe.id_proj = p.id_proj
    WHERE d.nama = 'RnD' AND p.status = 1;

![image](https://github.com/verz666/karyawan/assets/115523263/cf5fc02c-e869-4290-9361-5ce561fd422e)

## 4. Berapa banyak project yang sedang dikerjakan oleh Ari?

    SELECT COUNT(*) AS jumlah_project
    FROM Project_Employee pe
    INNER JOIN Employee e ON pe.nik = e.nik
    INNER JOIN Project p ON pe.id_proj = p.id_proj
    WHERE e.nama = 'Ari' AND p.status = 1;

![image](https://github.com/verz666/karyawan/assets/115523263/c1843714-9896-44e1-ba14-da8ebbb66f3a)

## 5. Siapa saja yang mengerjakan projcet B?

    SELECT e.nama
    FROM Project_Employee pe
    INNER JOIN Employee e ON pe.nik = e.nik
    INNER JOIN Project p ON pe.id_proj = p.id_proj
    WHERE p.nama = 'B';

![image](https://github.com/verz666/karyawan/assets/115523263/518fa568-07e8-487d-809c-435bdcd7926b)
