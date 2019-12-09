using System;
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class StressSystem
{

    private Character character;

    public event EventHandler OnStressChanged;
    public event EventHandler OnDead;

    private int stressMax;
    private int stress;

    public StressSystem(int stressMax)
    {
        this.stressMax = stressMax;
        stress = stressMax;
    }

    public void SetStressAmount(int stress)
    {
        this.stress = stress;
        if (OnStressChanged != null) OnStressChanged(this, EventArgs.Empty);
    }

    public float GetStressPercent()
    {
        return (float)stress / stressMax;
    }

    public int GetStressAmount()
    {
        return stress;
    }

    //Monsters will do stress damage
    public void StressDamage(int amount)
    {
        stress += amount;
        if (stress < 0)
        {
            stress = 0;
        }
        if (OnStressChanged != null) OnStressChanged(this, EventArgs.Empty);

        if (stress <= character.stats.stressMax)
        {
            Die();
        }
    }

    public void Die()
    {
        if (OnDead != null) OnDead(this, EventArgs.Empty);
    }

    public bool IsDead()
    {
        return stress <= 0;
    }

    //Stress heals the palyer
    public void StressHeal(int amount)
    {
        stress -= amount;
        if (stress > character.stats.stressMax)
        {
            stress = character.stats.stressMax;
        }
        if (OnStressChanged != null) OnStressChanged(this, EventArgs.Empty);
    }

}
