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
izjosve@ijzosve:~$ irb
irb(main):001:1* class Person
irb(main):002:1*   attr_accessor :name
irb(main):003:0> end
=> nil
irb(main):004:0> p = Person.new
irb(main):005:0> p.name = "ijzosve"
irb(main):006:0> p
=> #<Person:0x000055b382dc13e8 @name="ijzosve">
irb(main):007:0> Marshal.dump(p)
=> "\x04\bo:\vPerson\x06:\n@nameI\"\fijzosve\x06:\x06ET"
irb(main):008:0> Marshal.load("\x04\bo:\vPerson\x06:\n@nameI\"\fijzosve\x06:\x06ET")
=> #<Person:0x000055b383081e98 @name="ijzosve">
```
