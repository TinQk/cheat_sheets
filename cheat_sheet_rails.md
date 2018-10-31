# CHEAT SHEET RAILS
## RAILS - ACTIVERECORD - POSTGRESQL
<br>

### Init

Initialisation dossier rails :<br>
`$ rails new nom_du_projet`

Ou en précisant qu'on utilise postgresql (et pas sqlite3) :<br>
`$ rails new -d postgresql nom_du_project`

Installer toutes les gems du gemfile :
`$ bundle install`

### Console

Lancer la console pour s'amuser avec la base de donnée :<br>
`$ rails console` ou `$ rails c`

#### CRUD : Create Read Update Delete

* Créer un User en base :<br>
`User.create(name:"Jean-Michel", email:"jm@gmail.com")`
ou
```ruby
truc = User.new
truc.name = "Jean-Michel"
truc.save
```

* Récupère le User dont l'id est 4 (READ) :<br>
`User.find(4)`
* Update un truc :<br>
`truc.update(...)`
* Supprimer un truc :<br>
`truc.delete` supprime un truc de la bd


### Migrations

Gérer une base de données dans rails se fait via des migrations (dossier db) :

Créér une table :<br>
`$ rails generate migration CreateTableName` ou `$ rails g migration CreateTableName`

Créer une table de jointure : `$ rails g `

* Les noms de migrations sont en CamelCase.
* Les migrations sont créées dans le dossier db
* Les migrations peuvent créer des tables ou modifier des tables existantes

ex d'une migration qui crée une table "users" :

```ruby
class CreateUsers < ActiveRecord::Migration[5.2]
  def change
    create_table :users do |t|
      t.string :first_name
      t.string :last_name
    end
  end
end
```

Tout se passe dans "def change". A la place de create_table on peut avoir d'autres commandes :
* add_reference :column_name, :table_name
<br> --> rajoute une colonne à une table existante
* add_reference :books, :author, foreign_key: true
<br> --> rajoute la clé "author" à la table "book"



Executer les migrations (= créer ou modifier la base de donnée) :<br>
`$ rails db:migrate pour faire la migration`


### MVC = Model View Controller

### Models :

Les modèles récupérent les infos depuis la db pour permettre aux view de les utiliser.

Créer un modèle et la migration correspondante :
`$ rails g model NomDuModel`



### Lier deux tables en bd : (2 étapes)

#### Relation 1-1 ou 1-n

- Faire une migration qui va ajouter la clé étrangère dans la table qui représente l'objet qui appartiendra à l'autre objet (cf partie migration)

- Lier nos tables dans les models en utilisant :
    --> belongs_to :author
    --> has_many :chapters
    --> has_and_belongs_to_many :tags


Vérifier que deux tables sont liés via la console :


#### Relation n-n

Une table de jointure doit exister entre les deux :
- Si elle existe :
`has_many, through`


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
