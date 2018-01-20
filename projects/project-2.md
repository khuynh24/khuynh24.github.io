---
layout: project
type: project
image: images/pokemon_battle.jpg
title: Pokemon Battle Game
permalink: projects/vacay
# All dates must be YYYY-MM-DD format!
date: 2017-11-03
labels:
  - Java
  - GitHub
summary: A text-based interactive Pokemon game I developed in ICS 211.
---

<img class="ui medium right floated rounded image" src="../images/poke_begin">

Pokémon Battle Game is a two-player game that uses Pokémon object classes I created in ICS 211, Fall 2017. The project helped me learn how to design and implement various generic class objects and manage different methods to allow users-selection. I also learned how to keep track of user data after alternating turns.

The objective of the game is to terminate the other player first, before they terminate you. 

At the beginning of the game, each player chooses a Pokémon and randomly receives HP points (bounded depending on the Pokémon type). After both Pokémon are chosen, the game should randomly choose which Player goes first. Then the two players alternate, entering commands to attack until one Pokémon "faints" (reaches 0 HP). The options given to each player are "perform fastAttack", "perform specialAttack", and "pass" (Three passes allows the user to perform specialAttack). Each Pokémon have specific attacks types that are effective to a certain degree toward other Pokémon types. In other words, after a user performs an attack, it will decrement the other players HP by a certain degree, depending on both player Pokémon types.

Once a player's Pokémon has fainted, the game ends and print out a congratulatory message to the winner. 

<img class="ui medium right floated rounded image" src="../images/poke_end">


----------------------------------------------------------------------------------------------------------------------------


A snippet of code that shows what happens after a user chooses an attack. A switch statement is used to determine which method to perform. It also updates HP of each player and alternates the turns.
         
         switch(inString){
            // fastAttack Method
            case "1"://performs fast attack
               System.out.println(attacker.performFastAttack(victim)); 
               hp = hpChecker(hp, attacker, victim, player);//updates hp
               player = resetPlayer(player, player1, player2, attacker, victim);//updates player: attacker&victim   
               break;          
            // specialAttack method, test if attacker passes 3 times;
            case "2"://Special
               if(pass > 2){
                  if (player == 1){
                     passPlayer1 = passPlayer1 - 3;
                     System.out.println(attacker.performSpecialAttack(victim));
                     
                  }       
                  else{
                     passPlayer2 = passPlayer2 - 3;
                     System.out.println(attacker.performSpecialAttack(victim));
                  }
                  hp = hpChecker(hp, attacker, victim, player);//updates hp
                  player = resetPlayer(player, player1, player2, attacker, victim);//updates player: attacker&victim 
               }
               else{// Prints if not enough passes
                  System.out.println("You need 3 passes to perform special attack! You have " + pass + ". Try again");
               }               
               break;
            case "3":// Pass; increment player's number of passes
               if (player == 1)
                  passPlayer1++;
               else
                  passPlayer2++;
               player = resetPlayer(player, player1, player2, attacker, victim);//updates player: attacker&victim 
               break;
            default: //invalid menu entry: notify user
               System.out.println("\n****Invalid menu choice.****\nPlease enter a 0, 1, or 2\n");
               player = resetPlayer(player, player1, player2, attacker, victim);//updates player: attacker&victim
               break;        
         }//switch
