# Basic Weapon System In Unity

This tutorial shows how to create an easily expandable weapon system in Unity.

## 1. Set up scene

Under your player create a new game object and call it `Gun`, this will act as the object that we use to contain all of the logic of the weapon script.

Now create a new layer and call it `Enemy`, this will act as the enemy layer so the weapon can identify what the targets are.

## 2. Create weapon script

Under your scripts folder create a new script and call it `GunSystem`.

In this script we need to create the variales to control the properties of the gun:

```.cs
    public float timeBetweenShooting;
    public float spread;
    public float range;
    public float reloadTime;
    public float timeBetweenShots;
    public int magazineSize;
    public int bulletsPerTap;
    public bool allowButtonHold;
    private int _bulletsLeft, _bulletsShot;
```
