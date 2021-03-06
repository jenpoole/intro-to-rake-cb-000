# namespace a Rake task
# A namespace is a way to group or contain something, in this case our Rake tasks
namespace :greeting do
  desc 'outputs hello to the terminal'
  task :hello do
    puts "hello from Rake!"
  end

  desc 'outputs hola to the terminal'
  task :hola do
    puts "hola de Rake!"
  end
end

task :environment do
  require_relative './config/environment'
end

namespace :db do
  desc 'migrate changes to your database'
  task :migrate => :environment do
    Student.create_table
  end

  desc 'seed the database with some dummy data'
  task :seed do
    require_relative './db/seeds.rb'
  end
end

desc 'drop into the Pry console'
task :console => :environment do
  Pry.start
end

=begin
  Use rake tasks:
    rake greeting:hello
    rake greeting:hola
    rake db:migrate
    rake db:seed
    rake console

  RAKE DB:MIGRATE
  `task :migrate => :environment do` creates a task dependency.
  Since our Student.create_table code would require access to the config/environment.rb file (which is where the student class and database are loaded), we need to give our task access to this file. In order to do that, we need to define yet another Rake task that we can tell to run before the migrate task is run.

  RAKE DB:SEED
  The conventional way to seed your database is to have a file in the db directory, db/seeds.rb, that contains some code to create instances of your class. We define a rake task that executes the code in this file. This task will also be namespaced under db.

  RAKE CONSOLE
  We'll define a task that starts up the Pry console. We'll make this task dependent on our environment task so that the Student class and the database connection load first.

  rake console
  [1] pry(main)> Student.all
  => [[1, "Melissa", "10th"],
   [2, "April", "10th"],
   [3, "Luke", "9th"],
   [4, "Devon", "11th"],
   [5, "Sarah", "10th"]]
=end
