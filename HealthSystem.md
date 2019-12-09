using System;
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class HealthSystem {

    private Character character;

    public event EventHandler OnHealthChanged;
    public event EventHandler OnDead;

    private int healthMax;
    private int health;

    public HealthSystem(int healthMax) {
        this.healthMax = healthMax;
        health = healthMax;
    }

    public void SetHealthAmount(int health) {
        this.health = health;
        if (OnHealthChanged != null) OnHealthChanged(this, EventArgs.Empty);
    }

    public float GetHealthPercent() {
        return (float)health / healthMax;
    }

    public int GetHealthAmount() {
        return health;
    }
    //This is for lowering the health of the character
    public void Damage(int amount) {
        health -= amount;
        if (health < 0) {
            health = 0;
        }
        if (OnHealthChanged != null) OnHealthChanged(this, EventArgs.Empty);

        if (health <= 0) {
            Die();
        }
    }

    //If the hp reaches to 0 this is make it that the character dies.
    public void Die() {
        if (OnDead != null) OnDead(this, EventArgs.Empty);
    }

    public bool IsDead() {
        return health <= 0;
    }

    //Heals the player
    public void Heal(int amount) {
        health += amount;
        if (health > healthMax) {
            health = healthMax;
        }
        if (OnHealthChanged != null) OnHealthChanged(this, EventArgs.Empty);
    }

}
