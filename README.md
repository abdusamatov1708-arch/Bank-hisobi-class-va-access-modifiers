# Bank-hisobi-class-va-access-modifiers
TypeScript
// 1. Interfeys e'lon qilish
interface ChopEtiluvchi {
    malumotniChopEtish(): void;
}

// 2. Abstract class yaratish va interfeysni implements qilish
abstract class Shaxs implements ChopEtiluvchi {
    public ism: string;

    constructor(ism: string) {
        this.ism = ism;
    }

    // Abstract metod (avlod class buni majburiy bajarishi shart)
    abstract malumotniChopEtish(): void;
}

// 3. Abstract class'dan meros oluvchi class
class VIPMijoz extends Shaxs {
    constructor(ism: string) {
        super(ism);
    }

    // Abstract metod amalga oshirildi
    public malumotniChopEtish(): void {
        console.log(`VIP Mijoz ismi: ${this.ism}`);
    }
}

// 4. BankHisobi class'i
class BankHisobi {
    public egasi: string;        // Hamma joydan ko'rinadi
    private balans: number;       // Faqat shu class ichidangina ko'rinadi
    protected hisobRaqami: string; // Class va uning avlodlarida ko'rinadi

    constructor(egasi: string, boshlangichBalans: number, hisobRaqami: string) {
        this.egasi = egasi;
        this.balans = boshlangichBalans;
        this.hisobRaqami = hisobRaqami;
    }

    // Balansni xavfsiz o'qish uchun metod (Getter)
    public balansniKorish(): number {
        return this.balans;
    }

    // Balansni to'ldirish (Validatsiya bilan)
    public pulQoshish(summa: number): void {
        if (summa > 0) {
            this.balans += summa;
            console.log(`${summa} so'm qo'shildi. Joriy balans: ${this.balans}`);
        }
    }

    // Pul yechish (Xavfsizlik tekshiruvi bilan)
    public pulYechish(summa: number): boolean {
        if (summa > 0 && this.balans >= summa) {
            this.balans -= summa;
            console.log(`${summa} so'm yechildi. Qoldiq: ${this.balans}`);
            return true;
        }
        console.log("Xatolik: Mablag' yetarli emas yoki noto'g'ri summa!");
        return false;
    }
}

/*
  ------------------------------------------------------------
  PRIVATE XUSUSIYATGA TASHQARIDAN KIRISH XATOSI
  ------------------------------------------------------------
  const hisob = new BankHisobi("Aziz", 10000, "TR-98765");
  hisob.balans = 500000; // XATO!
  
  IZOH: TypeScript bu yerda kompilyatsiya xatosini beradi:
  "Property 'balans' is private and only accessible within class 'BankHisobi'."
  Sababi `private` kalit so'zi balans maydonini tashqi aralashuvlardan 
  qattiq himoya qiladi va uni faqat klass ichidagi metodlar orqali 
  boshqarishga ruxsat beradi.
*/

// --- Kodni sinab ko'rish ---

const mijoz = new VIPMijoz("Sardor");
mijoz.malumotniChopEtish(); // VIP Mijoz ismi: Sardor

const hisobKitob = new BankHisobi("Sardor", 5000, "UZ88888");
console.log(`Hisob egasi: ${hisobKitob.egasi}`);
console.log(`Boshlang'ich balans: ${hisobKitob.balansniKorish()}`);

hisobKitob.pulQoshish(2000); // 2000 so'm qo'shildi...
hisobKitob.pulYechish(3000);  // 3000 so'm yechildi...
