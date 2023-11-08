import os
from datetime import datetime

# kelola akun user
login_user = [{"username": "arif", "password": "123"}]

# akun admin
login_admin = [{"username": "admin", "password": "admin"}]


# Data roti
data_roti = [
    {"nama roti": "roti abon", "harga": 5000, "stok": 12},
    {"nama roti": "roti keju", "harga": 8000, "stok": 10},
    {"nama roti": "roti sosis", "harga": 12000, "stok": 7},
    {"nama roti": "roti blubery", "harga": 13000, "stok": 9},
    {"nama roti": "roti kacang", "harga": 10000, "stok": 4},
    {"nama roti": "roti kacang merah", "harga": 14000, "stok": 12},
]

# Fungsi untuk registrasi user
def registrasi_pengguna(username, password):
    login_user.append({'username': username, 'password': password})
    print("Registrasi berhasil.")

# fungsi untuk login akun
def login(username, password):
    for user in login_admin:
        if user['username'] == username and user['password'] == password:
            admin_menu()
            return True
    for user in login_user:
        if user['username'] == username and user['password'] == password:
            menu_user()
            print(f"Selamat datang, {username}!")
            return True
    print("Username atau password salah.")
    return False

# Fungsi untuk menambah jenis roti(termasuk harga dan stoknya)
def tambah_jenis_roti():
    nama_roti = []
    for i in data_roti:
        nama_roti.append(i["nama roti"])
    while True:
        try:
            jenis_roti = input("Masukkan nama roti: ").lower()
            if jenis_roti in nama_roti:
                print("Jenis roti ini sudah ada")
            else:
                try:
                    harga_roti = int(input("Masukkan Harga Roti: "))
                    if harga_roti <= 0:
                        print("harga tidak kurang dari 0")
                    else:
                        try:
                            stok_roti = int(input("Masukkan stok roti: "))
                            if stok_roti <= 0:
                                print("stok tidak kurang dari nol")
                            else:
                                data_roti.append(
                                    {
                                        "nama roti": jenis_roti,
                                        "harga": harga_roti,
                                        "stok": stok_roti,
                                    }
                                )
                                print("roti telah ditambahkan")
                                break
                        except ValueError:
                            print("Stok harus berupa angka")
                except ValueError:
                    print("Harga harus berupa angka")
        except ValueError:
            print("Nama roti harus berupa huruf")

# Fungsi untuk menampilkan seluruh menu roti mulai dari ID, jenis roti, harga roti, stok roti
def tampilkan_menu_roti():
    for id, roti in enumerate(data_roti, start =+ 1):
        print("ID\t\t: ", id)
        print("Jenis Roti\t: ", roti["nama roti"])
        print("Harga Roti\t: ", roti["harga"])
        print("Stok Roti\t: ", roti["stok"])
        print("\n")

# Fungsi untuk menampilkan seluruh menu roti mulai dari ID, jenis roti, harga roti, stok roti
def tampilkan_harga_roti():
    for id, roti in enumerate(data_roti, start=+1):
        print("ID\t\t: ", id)
        print("Jenis Roti\t: ", roti["nama roti"])
        print("Harga Roti\t: ", roti["harga"])
        print("\n")

# Fungsi untuk menampilkan seluruh menu roti mulai dari ID, jenis roti, harga roti, stok roti
def tampilkan_menu_roti():
    print("-" * 50)
    print("{:<3} | {:<20} | {:<10} | {:<5}".format("ID", "Jenis Roti", "Harga", "Stok"))
    print("-" * 50)
    for id, roti in enumerate(data_roti, start=1):
        jenis_roti = roti["nama roti"]
        harga_roti = roti["harga"]
        stok_roti = roti["stok"]
        print("{:<3} | {:<20} | {:<10} | {:<5}".format(id, jenis_roti, harga_roti, stok_roti))
    print("-" * 50)

        
# Fungsi untuk menampilkan seluruh list user
def list_user():
    os.system("cls")
    for no,user in enumerate(login_user, start=1):
        print(f"{no}. username: {user['username']}")

# Fungsi untuk mengupdate harga roti yang terdapat
def update_harga_roti():
    while True:
        tampilkan_harga_roti()
        try:
            pilih = int(input("Masukkan ID roti: "))
            if pilih > 0 and pilih <= len(data_roti):
                try:
                    harga_roti = int(input("Masukkan harga terbaru Roti: "))
                    if harga_roti >= 0:
                        data_roti[pilih - 1]["harga"] = harga_roti
                        print(
                            f"Harga {data_roti[pilih - 1]['nama roti']} berhasil di update"
                        )
                    else:
                        print("Harga roti kurang dari 0")
                except ValueError:
                    print("Harga berupa angka")
            else:
                print("Tolong masukkan id yang tepat")
            break
        except ValueError:
            print("ID Merupakan angka")

# Fungsi untuk mengupdate stok roti yang ada
def update_stok_roti():
    os.system("cls")
    while True:
        try:
            pilih = int(input("Masukkan ID roti: "))
            if pilih > 0 and pilih <= len(data_roti):
                while True:
                    try: 
                        stok_roti = int(input("Masukkan stok terbaru roti: "))
                        if stok_roti > 0:
                            data_roti[pilih - 1]["stok"] = stok_roti
                            print("Stok roti berhasil di-update")
                            break
                        else:
                            print("Stok roti tidak kurang dari 0")
                    except ValueError:
                        print("Stok berupa angka")
            else:
                print("Masukkan ID yang tepat!")
            break
        except ValueError:
            print("ID Merupakan angka")

# Fungsi untuk menambah belanjaan roti
def tambah_belanjaan():
    global belanja
    belanja = []
    while True:
        tampilkan_menu_roti()
        try: 
            item = int(input("Masukkan ID roti yang ingin dibeli\t: "))
            if item > 0 and item <= len(data_roti):
                try:
                    while True:
                        jumlah = int(input("masukkan Jumlah item yang ingin dibeli\t: "))
                        if jumlah > 0:
                            if jumlah <= data_roti[item - 1]["stok"]:
                                data_roti[item - 1]["stok"] -= jumlah
                                belanjaan = {
                                    'Item' : data_roti[item -1]["nama roti"],
                                    "Jumlah" : jumlah,
                                    "Harga": data_roti[item - 1]["harga"],
                                    "Total Harga": data_roti[item - 1]["harga"] * jumlah
                                } 
                                belanja.append(belanjaan)
                                break
                            else:
                                print(f"Stok {data_roti[item - 1]['nama roti']} tersisa {data_roti[item - 1]['stok']}")
                        else:
                            print("Jumlah item harus lebih dari 0")
                except ValueError:
                    print("Jumlah item berupa angka")
            else:
                print("Masukkan ID yang tepat")
            lanjut_pembelian = input("Ketik y jika ingin melanjutkan pembelian: ").lower()
            os.system('cls')
            if lanjut_pembelian != "y":
                break
        except ValueError:
            print("ID merupakan angka")
            
# Fungsi untuk menghitung total belanjaan
def hitung_belanjaan():
    total_belanja = 0
    for i in belanja:
        total_belanja += i['Total Harga']
    print("\tTotal :\t", total_belanja)

# fungsi untuk mencetak struk belanjaan
def struk_pembelian():
    print("-" * 20)
    print(f"User: {username}")
    print(f"Tanggal: {datetime.now().strftime('%x')} ")
    print(f"jam: {datetime.now().strftime('%H:%M %p')}\n")
    for struk in belanja:
        print(struk["Item"])
        print((struk["Jumlah"]), "pcs\t x\t", (struk["Harga"]), end="")
        # print(f"{struk['Jumlah']}    PCS  \tx {struk['Harga']}", end="")
        print(f":\t {struk['Total Harga']}")
    print("-" * 20)
    hitung_belanjaan()

# Fungsi menu admin
def admin_menu():
    os.system("cls")
    while True:
        print("===============================================")
        print("               MENU ADMIN CAKEP                ")
        print("===============================================")
        print("Pilihan Menu:")
        print("1. Tambahkan Jenis Roti")
        print("2. Tampilkan Seluruh Menu Roti yang Ada")
        print("3. Tampilkan Seluruh List User")
        print("4. Update Harga Roti yang Ada di Menu")
        print("5. Update Stok Roti yang Ada di Menu")
        print("6. Tampilkan Riwayat Pesanan")
        print("7. Keluar")
        print("===============================================")
        pilihan = input("Pilih Menu yang diinginkan: ")
        
        if pilihan == "1":
            tambah_jenis_roti()
        elif pilihan == "2":
            tampilkan_menu_roti()
        elif pilihan == "3":
            list_user()
        elif pilihan == "4":
            update_harga_roti()
        elif pilihan == "5":
            update_stok_roti()
        #elif pilihan == "6":
            #tampilkan_riwayat_pesanan() 
        elif pilihan == "7":
            os.system("cls")
            print("Terimakasih telah berkunjung, Semoga harimu menyenangkan:)")
            break
        else:
            print("Pilihan tidak valid. Silakan masukkan angka antara 1 dan 7.")
# Fungsi menu user
def menu_user():
    os.system("cls")
    while True:
        print("======================================")
        print("               MENU                   ")
        print("======================================")
        print("1.Tampilkan Menu Roti")
        print("2.Belanja")
        print("3.Exit")
        print("======================================")
        pilihan = input("Pilih Menu: ")
        if pilihan == "1" :
            tampilkan_menu_roti()
        elif pilihan == "2" :
            tambah_belanjaan()
            struk_pembelian()
        elif pilihan == "3" :
            os.system("cls")
            print("Terimakasih telah berkunjung, Semoga Harimu menyenangkan")
            break
# Fungsi menu utama
def menu_utama():
    os.system("cls")
    while True:
        print("===================================")
        print("           SELAMAT DATANG          ")
        print("===================================")
        print("1. Login")
        print("2. Registrasi")
        print("3. Exit")
        print("===================================")
        pilihan = input("Masukkan pilihan anda: ")

        if pilihan == '1':
            global username
            username = input("Masukkan username: ")
            password = input("Masukkan password: ")
            if login(username, password):
                print()
        elif pilihan == '2':
            username = input("Masukkan username: ")
            password = input("Masukkan password: ")
            registrasi_pengguna(username, password)
        elif pilihan == '3':
            break
        else:
            print("Opsi tidak valid. Coba lagi.")
        


menu_utama()
