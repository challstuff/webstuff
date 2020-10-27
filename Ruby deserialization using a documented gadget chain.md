# Ruby deserialization using a documented gadget chain
- Même principe que la déserialisation PHP, sauf que là on utilise le langage Ruby comme intermédiaire.<br/>
## Reconnaissance
- Je laisse tourner burpsuite en arrière-plan pendant que je me login avec les identifiants précisés dans l'énoncé.<br/></br>
<img src="https://media.discordapp.net/attachments/768928242467340328/770030149490966548/unknown.png"/><br/><br/>
- Je check l'historique des requêtes et je sélectionne l'index où le procédé du login a été sérialisé.<br/><br/>
<img src="https://media.discordapp.net/attachments/768928242467340328/770031231060017192/unknown.png?width=1195&height=890"/><br/><br/>
## Développement gadget 
- Pour commencer, un peu de théorie. Les termes utilisés par Ruby pour désigner la sérialisation et la désérialisation sont marshalling et unmarshalling.
- La classe Marshal a les méthodes de classe «dump» et «load» qui peuvent être utilisées comme suit:
```ruby
$ irb
>> class Person
>>   attr_accessor :name
>> end
=> nil

>> p = Person.new
=> #<Person:0x00005584ba9af490>

>> p.name = "Luke Jahnke"
=> "Luke Jahnke"

>> p
=> #<Person:0x00005584ba9af490 @name="Luke Jahnke">

>> Marshal.dump(p)
=> "\x04\bo:\vPerson\x06:\n@nameI\"\x10Luke Jahnke\x06:\x06ET"

>> Marshal.load("\x04\bo:\vPerson\x06:\n@nameI\"\x10Luke Jahnke\x06:\x06ET")
=> #<Person:0x00005584ba995dd8 @name="Luke Jahnke">
```
