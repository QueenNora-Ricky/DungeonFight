using System.Collections;
using System.Collections.Generic;
using UnityEngine;

/*
 * Represents a single character: Player, Companion, Enemy
 * */
public class Character
{

    public static bool IsUniqueCharacterType(Type type)
    {
        switch (type)
        {
            default:
            case Type.Player:

                return true;
            case Type.Enemy_Ghoul:
            case Type.Enemy_Orc:
            case Type.Enemy_Zombie:
                return false;
        }
    }


    public class Stats
    {
        public int healthMax;
        public int health;
        public int stressMax;
        public int stress;
        public int speedMax;
        public int speed;
        public int stressAttack;
        public int attack;
        public int manaMax;
        public int mana;

    }

    public enum Type
    {
        Player,

        Enemy_Ghoul,
        Enemy_Orc,
        Enemy_Zombie,
    }

    public Type type;
    public Stats stats;
    public string name;
    public Vector3 position;
    //public GameData.EnemyEncounter enemyEncounter;
    public bool isDead;
    public bool isInPlayerTeam;

    //Giving stats for each type of characters based on type
    public Character(Type type)
    {
        this.type = type;
        name = type.ToString();

        stats = new Stats
        {
            attack = 10,
            stressAttack = 5,
            health = 100,
            healthMax = 100,
            stress = 100,
            stressMax = 100,
            mana = 50,
            manaMax = 50,
            speed = 1,
            speedMax = 1,
        };

        switch (type)
        {
            default:
                Debug.Log("###### Default Type: " + type);
                break;
            case Type.Player:
                stats = new Stats
                {
                    attack = 35,
                    stressAttack = 0,
                    health = 150,
                    healthMax = 150,
                    stress = 0,
                    stressMax = 100,
                    mana = 50,
                    manaMax = 50,
                    speed = 1,
                    speedMax = 1,
                };
                isInPlayerTeam = true;
                break;
            case Type.Enemy_Ghoul:
                stats = new Stats
                {
                    attack = 10,
                    stressAttack = 15,
                    health = 50,
                    healthMax = 50,
                    stress = 0,
                    stressMax = 0,
                    mana = 0,
                    manaMax = 0,
                    speed = 1,
                    speedMax = 1,
                };
                break;
            case Type.Enemy_Orc:
                stats = new Stats
                {
                    attack = 35,
                    health = 100,
                    healthMax = 80,
                    stress = 0,
                    stressMax = 0,
                    mana = 0,
                    manaMax = 0,
                    speed = 1,
                    speedMax = 1,
                };
                break;
            case Type.Enemy_Zombie:
                stats = new Stats
                {
                    attack = 15,
                    stressAttack = 10,
                    health = 120,
                    healthMax = 120,
                    stress = 0,
                    stressMax = 0,
                    mana = 0,
                    manaMax = 0,
                    speed = 1,
                    speedMax = 1,
                };
                break;
        }
        isDead = false;
    }

    public bool IsEnemy()
    {
        switch (type)
        {
            default:
            case Type.Player:
                return false;
            case Type.Enemy_Ghoul:
            case Type.Enemy_Orc:
            case Type.Enemy_Zombie:
                return true;
        }
    }

}
