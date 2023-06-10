# ERD-karyawan

![image](https://github.com/verz666/karyawan/assets/115523263/c6a7e8df-8082-485f-afae-1fede06aaecb)

## table departemen

    CREATE TABLE Departemen (
    IDDepartemen INT PRIMARY KEY,
    NamaDepartemen VARCHAR(255)
    );

![image](https://github.com/verz666/karyawan/assets/115523263/9955dc20-29be-4541-9317-665f98194cc8)

## table karyawan

    CREATE TABLE Karyawan (
    IDKaryawan INT PRIMARY KEY,
    NamaKaryawan VARCHAR(255),
    IDSupervisor INT,
    IDDepartemen INT,
    FOREIGN KEY (IDSupervisor) REFERENCES Karyawan(IDKaryawan),
    FOREIGN KEY (IDDepartemen) REFERENCES Departemen(IDDepartemen)
    );

![image](https://github.com/verz666/karyawan/assets/115523263/705ce4e6-6a45-47e8-ba65-d49b4c155ce3)

## table proyek

    CREATE TABLE Proyek (
    IDProyek INT PRIMARY KEY,
    NamaProyek VARCHAR(255),
    TanggalMulai DATE,
    TanggalSelesai DATE
    );

![image](https://github.com/verz666/karyawan/assets/115523263/ffaad4f2-d9d7-4661-a9e3-060fb66b0caa)

## table supervisor

    CREATE TABLE Supervisor (
    IDSupervisor INT,
    IDDepartemen INT,
    FOREIGN KEY (IDSupervisor) REFERENCES Karyawan(IDKaryawan),
    FOREIGN KEY (IDDepartemen) REFERENCES Departemen(IDDepartemen)
    );

![image](https://github.com/verz666/karyawan/assets/115523263/4af74ee9-fd47-41e9-bd4f-f08aefa24de1)

## table partisipasi

    CREATE TABLE Partisipasi (
    IDKaryawan INT,
    IDProyek INT,
    FOREIGN KEY (IDKaryawan) REFERENCES Karyawan(IDKaryawan),
    FOREIGN KEY (IDProyek) REFERENCES Proyek(IDProyek)
    );

![image](https://github.com/verz666/karyawan/assets/115523263/16cf8115-f071-431a-b761-3cb9aca45b51)
