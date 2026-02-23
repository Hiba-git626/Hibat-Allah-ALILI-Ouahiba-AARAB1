
import java.io.*;
import java.util.Scanner; 

public class Magazin {
     static Scanner sc = new Scanner(System.in);
        static int [] Id=new int [10];
        static String [] Nom=new String [10];
        static double [] Prix=new double [10];
        static int [] Quantité=new int [10];
        static int nbProduits = 0;
        static int prochainId = 1;
        static final String File="stock.txt";
        static Scanner sc = new Scanner(System.in);
        public static void main (String[] args){
            stock();
            static int choix;
            do{
                menu();
                choix=saisirInt("choix:");
                switch (choix){
                    case 1 -> ajouterProduit();
                    case 2 -> Afficherlinventairecomplet();
                    case 3 -> Rechercherunproduit();
                    case 4 -> Réaliserunevente();
                    case 6 -> Sauvegarderdonnées();
                    case 7 -> chargerStock();
                    default -> System.out.println("Choix invalide !");
                }
                while(choix != 5);
                Sauvegarderdonnées();
            }
        static void AfficherMenu (){
         system.out.println("MENU:");
         system.out.println("1. Réaliser une vente:");
         system.out.println("2. Afficher l'inventaire complet: ");
         system.out.println("3. Rechercher un produit (par nom): ");
         system.out.println("4. Réaliser une vente (avec mise à jour stock):");
         system.out.println("5.Afficher les alertes (stock bas < 5). ");
         system.out.println("6. Sauvegarder les données:");
         system.out.println("7. Quitter:");
        }
        static int saisirInt(String msg) {
          System.out.print(msg);
          return sc.nextInt();
    }

        static double saisirDouble(String msg) {
          System.out.print(msg);
          return sc.nextDouble();
    }

        static String saisirString(String msg) {
          System.out.print(msg);
          sc.nextLine();
          return sc.nextLine();
    }


        static void ajouterProduit() {

        if (nbProduits >= 10) {
            System.out.println("Stock plein !");
            return;
        }

        int id = prochainId++;
        String nom = saisirString("Nom : ");
        double p = saisirDouble("Prix : ");
        int q = saisirInt("Quantité : ");

        ids[nbProduits] = id;
        noms[nbProduits] = nom;
        prix[nbProduits] = p;
        quantites[nbProduits] = q;

        nbProduits++;

        System.out.println("Produit ajouté avec ID : " + id);
    }

    

    static void Afficherlinventairecomplet()() {

        if (nbProduits == 0) {
            System.out.println("Aucun produit !");
            return;
        }

        System.out.println("\nListe des produits :");

        for (int i = 0; i < nbProduits; i++) {
            System.out.println(
                    "ID: " + ids[i] +
                    " | Nom: " + noms[i] +
                    " | Prix: " + prix[i] +
                    " | Stock: " + quantites[i]
            );
        }
    }

    static void Réaliserunevente () {

        int id = saisirInt("ID produit : ");

        int index = chercherIndex(id);

        if (index == -1) {
            System.out.println("Produit introuvable !");
            return;
        }

        int qte = saisirInt("Quantité demandée : ");

        if (quantites[index] < qte) {
            System.out.println("Stock insuffisant !");
            return;
        }

        double total = prix[index] * qte;

        if (total > 1000) {
            total *= 0.9;
            System.out.println("Remise de 10% appliquée !");
        }

        quantites[index] -= qte;

        System.out.println("Total à payer : " + total + " DH");
    }

    static void Rechercher un produit(int id) {
        for (int i = 0; i < nbProduits; i++) {
            if (ids[i] == id) return i;
        }
        return -1;
    }


    static void Sauvegarderdonnées() {

        try (PrintWriter pw = new PrintWriter(new FileWriter(FICHIER))) {

            for (int i = 0; i < nbProduits; i++) {
                pw.println(ids[i] + ";" + noms[i] + ";" + prix[i] + ";" + quantites[i]);
            }

            System.out.println("Stock sauvegardé.");

        } catch (IOException e) {
            System.out.println("Erreur sauvegarde !");
        }
    }

    static void chargerStock() {
        File f = new File(FICHIER);

        if (!f.exists()) return;

        try (BufferedReader br = new BufferedReader(new FileReader(f))) {

            String ligne;
            int maxId = 0;

            while ((ligne = br.readLine()) != null) {

                String[] parts = ligne.split(";");

                ids[nbProduits] = Integer.parseInt(parts[0]);
                noms[nbProduits] = parts[1];
                prix[nbProduits] = Double.parseDouble(parts[2]);
                quantites[nbProduits] = Integer.parseInt(parts[3]);

                if (ids[nbProduits] > maxId)
                    maxId = ids[nbProduits];

                nbProduits++;
            }
            prochainId = maxId + 1;

            System.out.println("Stock chargé.");

        } catch (IOException e) {
            System.out.println("Erreur chargement !");
        }
    }
}
    


   
