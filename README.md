# Repos

#creating a weapon for character

    class Weapon:
        validWeapon = {"dagger":4,"axe":6,"staff":6,"sword":10,"none":1}
        def __init__(self,weaponType):
            self.weaponType = weaponType
            self.damage = Weapon.validWeapon[weaponType]
            
        def __str__(self):
            if self.weaponType in Weapon.validWeapon:
                return self.weaponType
            
#creating armor for character
   
   class Armor:
        validArmor = {"plate":2,"chain":5,"leather":8,"none":10}
        
        def __init__(self,armorType):
            self.armorType = armorType
            self.ac = Armor.validArmor[armorType]
        
        def __str__(self):
            if self.armorType in Armor.validArmor:
                return self.armorType
        
#class RPGCharacter

    class RPGCharacter:
        def __init__(self,name):
            self.name = name
            self.armor = Armor("none")
            self.weapon = Weapon("none")
            self.health = self.maxHealth
            self.spell = self.maxSpell

#check for defeat
    
    def checkForDefeat(self):
        if self.health <= 0:
            print(self.name,"has been defeated!")
        
#fight method
   
   def fight(self,other):
        print(self.name,"attacks",other.name,"with a(n)",self.weapon)
        other.health -= self.weapon.damage
        print(self.name,"does",self.weapon.damage,"damage to",other.name)
        print(other.name,"is now down to",other.health,"health")
            
    def __str__(self):
        outStr = "\n" + self.name
        outStr += "\n" + format("Current Health: ",">19s") + str(self.health)
        outStr += "\n" + format("Current Spell Points: ", ">25s") +\
                  str(self.spell)
        outStr += "\n" + format("Wielding: ", ">13s") + str(self.weapon)
        outStr += "\n" + format("Wearing: ", ">12s") + str(self.armor)
        outStr += "\n" + format("Armor Class: ", ">16s") +\
                  str(self.armor.ac) + "\n"
        return outStr

#wizard character class     

    class Wizard(RPGCharacter):
        maxHealth = 16
        maxSpell = 20
        validWeapon = {"dagger":4,"staff":6,"none":1}
            
#wizard wielding
    
    def wield(self,Weapon):
        if Weapon.weaponType in Wizard.validWeapon:
            self.weapon = Weapon
            print(self.name,"is now wielding a(n)",self.weapon)
        else:
            print("Weapon not allowed for this character class.")

#put on armor for wizard
    
    def putOnArmor(self,Armor):
        if Armor.ac != self.armor.ac:
            print("Armor not allowed for this character class")
        else:
            print(self.name,"is now wearing",self.armor)

    def takeOffArmor(self,Armor):
        print(Amrmor.ac)
        
#cast spell
    def castSpell(self,spellName,other):
        if spellName == "Fireball":
            cost = 3
            effect = 5
            print(self.name,"casts",spellName,"at",other.name)
            other.health -= effect
            self.spell -= cost
            print(self.name,"does",effect,"damage to",other.name)
            print(other.name,"is now down to",other.health,"health")
        elif spellName == "Lightning Bolt":
            cost = 10
            effect = 10
            print(self.name,"casts",spellName,"at",other.name)
            other.health -= effect
            self.spell -= cost
            print(self.name,"does",effect,"damage to",other.name)
            print(other.name,"is now down to",other.health,"health")
        elif spellName == "Heal":
            cost = 6
            effect = -6
            print(self.name,"casts",spellName,"at",other.name)
            other.health -= effect
            self.spell -= cost
            print(self.name,"heals",other.name,"for",abs(effect),"health points")
            print(other.name,"is now at",other.health,"health")
        else:
            print("Unknown spell name. Spell failed.")
        
#fighter character class
    class Fighter(RPGCharacter):
        maxHealth = 40
        maxSpell = 0
        validWeapon = {"dagger":4,"axe":6,"staff":6,"sword":10,"none":1}

#fighter wielding
    def wield(self,Weapon):
        if Weapon.weaponType in Fighter.validWeapon:
            self.weapon = Weapon
            print(self.name,"is now wielding a(n)",self.weapon)

#put on armor for fighter
    def putOnArmor(self,Armor):
        if Armor.ac != self.armor.ac:
            self.armor = Armor
            print(self.name,"is now wearing",self.armor)
        else:
            print(self.name,"is now wearing",self.armor)
        
def main():

    plateMail = Armor("plate")
    chainMail = Armor("chain")
    sword = Weapon("sword")
    staff = Weapon("staff")
    axe = Weapon("axe")

    gandalf = Wizard("Gandalf the Grey")
    gandalf.wield(staff)
    
    aragorn = Fighter("Aragorn")
    aragorn.putOnArmor(plateMail)
    aragorn.wield(axe)
    
    print(gandalf)
    print(aragorn)

    gandalf.castSpell("Fireball",aragorn)
    aragorn.fight(gandalf)

    print(gandalf)
    print(aragorn)
    
    gandalf.castSpell("Lightning Bolt",aragorn)
    aragorn.wield(sword)

    print(gandalf)
    print(aragorn)

    gandalf.castSpell("Heal",gandalf)
    aragorn.fight(gandalf)

    gandalf.fight(aragorn)
    aragorn.fight(gandalf)

    print(gandalf)
    print(aragorn)
    
main()
