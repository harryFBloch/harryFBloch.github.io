---
layout: post
title:      "has-many trough tutorial"
date:       2018-12-04 19:07:55 -0500
permalink:  has-many_trough_tutorial
---


For this tutorial I am going to show you to create a simple has_many through association using rails. Our Model will consist of 3 classes Paper, Paragraph, and Sentence.

* A Paper will have many Paragraphs and many Sentences through Paragraphs. 
* A Paragraph will belong to a Paper and have many Sentences
* A Sentence will belong to a Paragraph 

	Lets start off by creating our app with the rail new command and we will call our app has-through-tutorial
	
```
		In the Terminal enter  $ ralis new has-through-tutorial
```

	Next we will generate our models with the rails generator command. Make sure you cd into your project’s root directory and enter the follow in the terminal:
			
	```
$ rails g model paper
$ rails g model paragraph
$ rails g model sentence
```

	This will generate our model class files and migration files to create our tables. Open up the Paper migration file /db/migration/001create_papers.rb the numbers in from of create_papers will we different for you. Then add this line inside the create table block.
```
t.string :title
```
	Here we are adding the column title to our Papers table and model. Now in the same place on the create_sentance.rb migration file add this line. 
	
```
t.integer :paper_id
```

	Here we are adding the foreign key for the paper our paragraph belongs to.Now on to the create_sentace.rb migration file also in the create table block add:
	
```
t.integer :paragraph_id
t.string :text
```

	Here we are adding the foreign key for paragraph just like we did before with paper_id and we adding a column to the sentences table for text. Next in the terminal run:

```
$rake db:migrate
```

	This will run the migration files we just created and edited adding the tables to our database. Next open up app/models/paper.rb and add the association: 

```
has_many :paragraphs
has_many :sentences, through: :paragraphs
```

	Here we are setting up the has_many and has_many through association using the ActiveRecord methods. Now open up app/models/paragraph.rb, and add the correct associations: 

```
belongs_to :paper
has_many :sentances
```

	Just like before we are setting up another has many association however this time we are using a new method belongs_to telling ActiveRecord that each Paragraph has only one paper. Finally on to app/models/sentance.rb. 
			```
belongs_to :paragraph
```

	Now our associations are all set up add this to you seed file db/seeds.rb:
	
```
paper = Paper.create(title: "Hi")
paragraph = Paragraph.new()
sentance = Sentance.new(text: "Hello World!")
sentance.paragraph = paragraph
paragraph.paper = paper
paper.save
sentance.save
paragraph.save

paper = Paper.create(title: "second paper")
paragraph = Paragraph.new()
sentance = Sentance.new(text: "Hello World Again!")
sentance.paragraph = paragraph
paragraph.paper = paper
paper.save
sentance.save
paragraph.save
```


Now enter rails console by typing $ rails c in the terminal. And then enter:
```
p = Paper.all.first
p.paragraphs
```
Will return an array of paragraphs and if you enter p.sentences you will get an array of all the sentences in the paper. Congratulations your has many through association is all set up. You can use this same way of setting up associations with any has many through model. 

		
