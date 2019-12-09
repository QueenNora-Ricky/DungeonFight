using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class BattleSystem : MonoBehaviour{

    //I know I am missing variables needed for this.

    private Character character;
    private HealthSystem healthSystem;
    private StressSystem stressSystem;
    //private World_Bar healthBar;

    public enum BattleStates{
        START,
        BATTLENUM,
        PLAYERNUM,
        ENEMYNUM,
        DAMAGECOUNT,
        WIN,
        LOST
    }

    //If I want to have more than one enemy I can use a postion funtion which will be fixed postions that will spawn the enemies on that vector.
    //For example I have to postions Top and Bottom I can spawn in 2 enemies one at each spot.

    private BattleStates currentState;

    // Start is called before the first frame update
    void Start(){
        currentState = BattleStates.START;
        //healthBar = new World_Bar(transform, new Vector3(0, 10), new Vector3(12, 1.7f), Color.grey, Color.red, 1f, 100, new World_Bar.Outline { color = Color.black, size = .6f });
    }

    // Update is called once per frame
    void Update(){
        Debug.Log(currentState);
        switch (currentState){
            case (BattleStates.START):
                //create the enemies and player
                break;
            case (BattleStates.BATTLENUM):
                //What battle it is. Planning on 3
                break;
            case (BattleStates.PLAYERNUM):
                //Player chooses what to do
                //Choses what target
                if (Input.GetKeyDown(KeyCode.W))
                {

                }
                if (Input.GetKeyDown(KeyCode.S))
                {

                }
                //Normal attack
                if (Input.GetKeyDown(KeyCode.Space))
                {
                    healthSystem.Damage(character.stats.attack);
                    Debug.Log("Player Attacks With Normal Attack And Does " + character.stats.attack);
                }
                //Special AOE Attack
                if (Input.GetKeyDown(KeyCode.T))
                {
                    healthSystem.Damage(character.stats.attack - 10);
                    Debug.Log("Player Attacks With Special Attack And Does " + (character.stats.attack - 10));
                }
                //Meditate 
                if (Input.GetKeyDown(KeyCode.Y))
                {
                    stressSystem.StressHeal(45);
                    Debug.Log("Player Uses Meditate And Stress Heals For 45");
                }
                //Use potion
                if (Input.GetKeyDown(KeyCode.U))
                {
                    healthSystem.Heal(100);
                    Debug.Log("Player Uses A Potion And Heals For 100");
                }
                break;
            case (BattleStates.ENEMYNUM):
                //Enemy choice which is only to attack the player with a normal attack
                //I was planning on making a array for the enemies since there will be 2 enemies with this it will make sure all the enemies attacked
                //Planning on giving the ghoul a on death stress attack
                break;
            case (BattleStates.DAMAGECOUNT):
                //Calculate damage done
                //Also will determine if the player dies with if statements HP will be simple by reaching to 0
                //For stress it will be different just by adding a debuff which will apply when the player reaches 65% stress. Once the player reaches 100% they lose 90% of their current hp.
                //Also the BattleOver function will be called here to see if the condtions are made
                break;
            case (BattleStates.WIN):
                //if all enemies die then player wins
                //This is also where we see if the player won all the fights if not goes to the next battle by int
                break;
            case (BattleStates.LOST):
                //if player loses all thier hp or gains a certain amount of stress they lose
                break;
        }
    }

    /*private bool BattleOver()
    {
        if (When player is dead)
        {
            // Player dead, enemy wins
            Debug.Log("Player Loses");
            return true;
        }
        if (When all enemies are dead)
        {
            // Enemy dead, player wins
            Debug.Log("Player Wins");
            return true;
        }
        //If no one is dead
        return false;
    }*/
}
