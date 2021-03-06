# CHEAT SHEET RAILS
## RAILS - ACTIVERECORD - POSTGRESQL
<br>

### INIT

Initialisation dossier rails :<br>
`$ rails new nom_du_projet`

Ou en précisant qu'on utilise postgre (et pas sqlite3) (gem pg) :<br>
`$ rails new -d postgresql nom_du_project`

Installer toutes les gems du gemfile :
`$ bundle install`

Créer la base de donnée :
`$ rails db:create`

Démarrer un serveur rails pour les tests (localhost:3000/) :
`$ rails server`

<br>

### CONSOLE

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

Il existe aussi le modèle REST qui fait 7 choses sur les ressources.

#### Association

Pour associer une instance à une autre (et vérifier si la jointure marche) :<br>
* si relation avec n : `shakespeare.books << macbeth`
* sinon : `macbeth.author = shakespeare`

Puis pour check si ça a marché : `shakespeare.books`


<br>

### MIGRATIONS

**Gérer une base de données dans rails se fait via des migrations qui crées et modifient des tables. On les retrouve dans le dossier db.**
<br><br>

Executer les migrations générées (= créer ou modifier la base de donnée) :<br>
`$ rails db:migrate`

Vérifier si les migrations générées ont été éxecutées :<br>
`$ rails db:migrate:status`

Générer une migration qui crée une table :<br>
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


<br>

### MVC = MODEL VIEW CONTROLLER

#### Models :

Les modèles récupérent les infos depuis la db pour permettre aux view de les utiliser.

Créer un modèle et la migration correspondante :
`$ rails g model NomDuModel`
<br>

**Class name :** cours du jeudi semaine 4 à check

#### Routes :

* Le fichier routes.rb (dans config) redirige vers un controller en fonction de l'url demandée.

* Rails utilise le REST pour ses routes et controller, c'est à dire les méthode #new, #create, #show, #index, #edit, #update, #destroy. Ces méthodes représentent le CRUD.

* Il est possible et très facile de faire des routes qui suivent le REST avec resources.


Afficher toutes les routes de l'application : `$ rails routes`




Rails utilise 5 méthodes :

* GET : utilisée pour envoyer une page à un user qui demande une page
`get 'page_url', to: 'controller_name#method_name'`
ex : `get '/static_pages/contact', to: 'static_pages#contact'`
--> renvoyer vers la méthode 'contact' du controller 'StaticPages'

* POST : utilisée pour recevoir de l'information d'un utilisateur qui permet de créer une ressource en base

* PUT / PATCH : utilisées pour recevoir de l'information qui permet de mettre à jour une ressource en base

* DELETE : utilisée pour supprimer une ressource en base




#### Controllers :

Rails utilise le REST pour ses routes et controller, c'est à dire les méthode #new, #create, #show, #index, #edit, #update, #destroy. Ces méthodes représentent le CRUD.


Générer un controller (et sa view au passage) :<br>
`$ rails g controller controller_name method_name`
<br>
Exemple : `$ rails g controller static_pages home`





<br>

### LIER DEUX TABLES EN DB

#### Relation 1-1 ou 1-n : (2 étapes)

- Faire une migration qui va ajouter la clé étrangère dans la table qui représente l'objet qui appartiendra (belongs) à l'autre objet (cf partie migration)

- Lier nos tables dans les models en utilisant :
  - `belongs_to :truc`
  - `has_many :trucs`
  - `has_and_belongs_to_many :trucs`


#### Relation n-n : (2 étapes)

Une table de jointure doit exister entre les deux tables :

- Si elle existe, on vérifie qu'elle contient bien les clés étrangères des deux tables à joindre, et on ajoute has many through dans les deux modèles :<br>
`has_many :trucs, through: join_table`

- Si elle n'existe pas, on la crée via la commande :<br>
  `$ rails g migration CreateJoinTableTruc1Truc2 truc1 truc2`
  Puis dans les deux modèles on ajoute :<br>
  `has_and_belongs_to_many :trucs`


<br>

### SEED

Rempli une base de donnée avec des entrée pré-programmées ou random depuis le fichier : /db/seeds.rb
<br><br>

Un exemple de seed :

```ruby
100.times do |index|
    user = User.create!(name: "Nom#{index}", email: "email#{index}@example.com")
end
```

Commande pour run le fichier seeds.rb et remplir la bd :<br>
`$ rails db:seed  # remplir sa db de random`
<br>

**Faker** : gem qui permet de créer des faux noms. Ne pas oublier "require 'faker'" dans seeds.rb
<br>

Un exemple de seed malin en utilisant la gem Faker :

```ruby
require 'faker'
100.times do
    user = User.create!(name: Faker::Company.name, email: Faker::Internet.email)
end
```


<br>

### RAILS-ERD (SCHEMA)

Créer un SCHEMA de la base de donnée de rails en pdf :

1. Ajouter la gem au gemfile : `$ gem 'rails-erd'`

2. Installer graphviz sur l'ordinateur (ubuntu : `$ sudo apt-get install graphviz` )

3. Lancer la commande de création : `$ rake erd`

--> un pdf "erd.pdf" a été sauvegardé à la racine de votre projet rails.
