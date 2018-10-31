# CHEAT SHEET RAILS
## RAILS - ACTIVERECORD - POSTGRESQL
<br>

### Basics

Initialisation dossier rails :<br>
```
$ rails new nom_du_projet
```

Ou en précisant qu'on utilise postgresql (et pas sqlite3) :<br>
```
$ rails new -d postgresql nom_du_project
```


Installer toutes les gems du gemfile :
```
$ bundle install
```

Lancer la console pour s'amuser avec la base de donnée :<br>
```
$ rails console
```
ou
```
$ rails c
```

### Migrations :

Gérer une base de données dans rails se fait via des migrations (dossier db) :

    Créér une migration :
    $ rails generate migration NomDeTaMigration

    Les noms de migrations sont en CamelCase.
    Les migrations sont créées dans le dossier db
    Les migrations peuvent créer des tables ou modifier des tables existantes
    ex :
```
    class CreateUsers < ActiveRecord::Migration[5.2]
  def change
    create_table :users do |t|
      t.string :first_name
      t.string :last_name
```
    Executer les migrations (= créer ou modifier la base de donnée) :
    $ rails db:migrate pour faire la migration
```

### Models :

Les modèles récupérent les infos depuis la db pour permettre aux view de les utiliser.

    Créer un modèle et la migration correspondante :
    $ rails generate model NomDuModel



MVC = Model View Controller

Route :
Controller :
Model :
View :


ActiveRecord : permet de gérer la base de données en ruby. C'est le M de MVC. Tu peux appliquer ton CRUD avec les méthodes de ActiveRecord :

    CRUD :
    Create : avec #create
    Read : avec #find
    Update : avec #update
    Destroy : avec #destroy



Lier deux tables en bd : (2 étapes)

    - Faire une migration qui va ajouter la clé étrangère dans la table qui représente l'objet qui appartiendra à l'autre objet

    ex :book appartient à son author, donc c'est book qui aura la clé étrangère
    --> add_reference :books, :author, foreign_key: true


    - Lier nos tables dans les models en utilisant has_many et belongs_to
    --> belongs_to :author
    --> has_many :chapters
    --> has_and_belongs_to_many :tags


Vérifier que deux tables sont liés via la console :



SEED : Créer automatiquement des données random afin de tester une appli

    dans le fichier db/seeds.rb
    Voici un exemple de seed :
        100.times do |index|
            user = User.create!(name: "Nom#{index}", email: "email#{index}@example.com")
        end

    Run le fichier seeds.rb pour remplir la bd :
    rails db:seed  # remplir sa db de random

    Faker : gem qui permet de créer des faux noms. Ne pas oublier "require 'faker'" dans seeds.rb
    exemple de seed malin en utilisant la gem Faker :
        require 'faker'
        100.times do
            user = User.create!(name: Faker::Company.name, email: Faker::Internet.email)
        end



Créer un SCHEMA de la base de donnée de rails en pdf :

    1) Ajouter la gem au gemfile :
    gem 'rails-erd'

    2) Installer graphviz sur l'ordinateur (ubuntu : sudo apt-get install graphviz )

    3) Lancer la commande de création : rake erd

    --> un pdf "erd.pdf" a été sauvegardé à la racine de votre projet rails.
