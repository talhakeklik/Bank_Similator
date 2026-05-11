# Bank_Similator
A # Python Project

# Barış Şaman,           242010020014
# Halis Yiğit Karadeniz, 242010020013
# Talha Keklik,          242010020004

class Kullanici:
    def __init__(self):
        self.hesaplar = {}

    # üye ekleyen fonk
    def uye_ekle(self, hesap_no, isim):
        if hesap_no in self.hesaplar:
            print("This account number is already registered in the system.")
        else:
            # HATA BURADAYDI: "bakye" yerine "bakiye" olarak düzeltildi.
            self.hesaplar[hesap_no] = {"isim": isim, "bakiye": 0.00}
            print(f"Customer named {isim} has been successfully added with account number '{hesap_no}'. ")

    # üye silen fonk
    def uye_sil(self, hesap_no):
        if hesap_no in self.hesaplar:
            isim = self.hesaplar[hesap_no]["isim"]
            del(self.hesaplar[hesap_no])
            print(f"Customer named {isim} has been successfully removed from the system.")
        else:
            print("This account number is not registered in the system.")

    # para yatirma fonk
    def para_yatir(self, hesap_no, miktar):  # deposit
        if hesap_no in self.hesaplar:
            if miktar > 0:
                self.hesaplar[hesap_no]["bakiye"] += miktar
                guncel_bakiye = self.hesaplar[hesap_no]["bakiye"]
                print(f"{miktar} TL was deposited into the account.\nCurrent balance: {guncel_bakiye} TL")
        else:
            print("This account number is not registered in the system.")

    # para cekme fonk
    def para_cek(self, hesap_no, miktar):
        if hesap_no in self.hesaplar:
            mevcut_bakiye = self.hesaplar[hesap_no]["bakiye"]
            if miktar <= 0:
                print("The amount to be withdrawn must be greater than 0.")
            elif mevcut_bakiye >= miktar:
                self.hesaplar[hesap_no]["bakiye"] -= miktar
                guncel_bakiye = self.hesaplar[hesap_no]["bakiye"]
                print(f"{miktar} TL was withdrawn from the account. Remaining balance: {guncel_bakiye} TL")
            else:
                guncel_bakiye = self.hesaplar[hesap_no]["bakiye"]
                print(f"Insufficient balance! Your current balance: {guncel_bakiye} TL")
        else:
            print("This account number is not registered in the system.")

    # bakiye sorgulama fonk
    def bakiye_sorgula(self, hesap_no):
        if hesap_no in self.hesaplar:
            isim = self.hesaplar[hesap_no]["isim"]
            bakiye = self.hesaplar[hesap_no]["bakiye"]
            print(f"The current balance for the customer named {isim} is: {bakiye} TL")
        else:
            print("This account number is not registered in the system.")

# menü
def ana_menu():
    banka = Kullanici()

    while True:
        print("\n" + "=" * 30)
        print("WELCOME TO THE BANK SIMULATOR")
        print("=" * 30)
        print("1. Add Member")
        print("2. Delete Member")
        print("3. Deposit")
        print("4. Withdraw money")
        print("5. Check Balance")
        print("6. Exit")
        print("=" * 30)

        secim = input("Please select the action you wish to perform (1–6): ")

        if secim == '1':  # hesap ekleme
            hesap_no = input("Account Number to Be Created: ")
            isim = input("Customer's First and Last Name: ")
            banka.uye_ekle(hesap_no, isim)

        elif secim == '2':  # hesap silme
            hesap_no = input("Account Number to be Deleted: ")
            banka.uye_sil(hesap_no)

        elif secim == '3':  # para yatırma
            hesap_no = input("Account Number for Deposit: ")
            try:
                miktar = float(input("Quantity Number: "))
                banka.para_yatir(hesap_no, miktar)
            except ValueError:
                print("Please enter a valid number.")

        elif secim == '4':  # para çekme
            hesap_no = input("Account Number for Withdrawal: ")
            try:
                miktar = float(input("Amount To Be Withdrawn: "))
                banka.para_cek(hesap_no, miktar)
            except ValueError:
                print("Please enter a valid number.")

        elif secim == '5':  # bakiye sorgulama
            hesap_no = input("Account Number to be Queryed: ")
            banka.bakiye_sorgula(hesap_no)

        elif secim == '6':  # cıkıs
            print("Logging out. Have a good day.")
            break

        else:  # gecersiz sayı
            print("Invalid selection! Please enter a number between 1 and 6.")

if __name__ == "__main__":
    ana_menu()Python based Bank Account Simulator that handles user registration, deposits, withdrawals, and balance inquiries via a command line interface.
