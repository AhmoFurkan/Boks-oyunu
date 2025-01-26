# Boks-oyunu
Dövüşe ilk kimin başlayacağını hesaplayan program .

public class Main {

    public static void main(String[] args) {
        Fighter f1 = new Fighter("A", 10, 120, 100,40,70);
        Fighter f2 = new Fighter("B", 20, 85, 85,30,50);

        Match match = new Match(f1, f2, 85, 100);
        match.run();
    }

}
===============================================================================================
public class Match {
    Fighter f1;
    Fighter f2;
    int minWeight;
    int maxWeight;


    Match(Fighter f1, Fighter f2, int minWeight, int maxWeight) {
        this.f1 = f1;
        this.f2 = f2;
        this.maxWeight = maxWeight;
        this.minWeight = minWeight;

    }

    void run() {
        if (isCheck()) {
            while (this.f1.health > 0 && this.f2.health > 0) {
                System.out.println("====YENİ ROUND====");
                if ((f1.isDodge2())) {
                    this.f2.health = this.f1.hit(this.f2);
                }
                if (isWin()) {
                    break;
                }
                if (f2.isDodge2()) {
                    this.f1.health = this.f2.hit(this.f1);
                }
                if (isWin()) {
                    break;
                }
                System.out.println(this.f1.name + " Sağlık : " + this.f1.health);
                System.out.println(this.f2.name + " Sağlık : " + this.f2.health);
            }
        } else {
            System.out.println("Sporcuların sikletleri uymuyor.");
        }

    }

    boolean isCheck() {
        return (this.f1.weight >= minWeight && this.f1.weight <= maxWeight) && (this.f2.weight >= minWeight && this.f2.weight <= maxWeight);
    }

    boolean isWin() {
        if (this.f1.health == 0) {
            System.out.println(this.f2.name + " Kazandı ");
            return true;
        }

        if (this.f2.health == 0) {
            System.out.println(this.f1.name + " Kazandı ");
            return true;
        }
        return false;
    }


}
===============================================================================================================================
public class Fighter {
    String name;
    int damage;
    int health;
    int weight;
    int dodge;
    int dodge2;

    Fighter(String name, int damage, int health, int weight, int dodge,int dodge2) {
        this.name = name;
        this.damage = damage;
        this.health = health;
        this.weight = weight;
        if (dodge >= 0 && dodge <= 100) {
            this.dodge = dodge;
        } else {
            this.dodge = 0;
        }
        if (dodge2 >= 0 && dodge2 <= 100) {
            this.dodge2 = dodge2;
        } else {
            this.dodge2 = 0;
        }



    }

    int hit(Fighter foe) {
        System.out.println(this.name + " => " + foe.name + " " + this.damage + " hasar vurdu ");
        if (foe.isDodge()) {
            System.out.println(foe.name + " gelen hasarı blokladı ");
            System.out.println("--------");
            return foe.health;
        }
        if (foe.health - this.damage < 0) {
            return 0;
        }
        return foe.health - this.damage;
    }

    boolean isDodge() {
        double randomNumber = Math.random() * 100;
        return randomNumber <= this.dodge;
    }
    boolean isDodge2() {
        double randomNumber = Math.random() * 100;
        return randomNumber <= this.dodge2;
    }

}

