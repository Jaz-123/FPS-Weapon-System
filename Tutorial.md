# Basic Weapon System In Unity

This tutorial shows how to create an easily expandable weapon system in Unity.

## 1. Set up scene

Under your player create a new game object and call it `Gun`, this will act as the object that we use to contain all of the logic of the weapon script.

Now create a new layer and call it `Enemy`, this will act as the enemy layer so the weapon can identify what the targets are.

## 2. Create weapon script

Under your scripts folder create a new script and call it `GunSystem`.

### Refrences

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

These variables control the variables such as bullet spread, range, reload and fire rate.

Now we need to create some variaes for the refrences we could need for the script:

```.cs
    public Camera fpsCam;
    public LayerMask whatIsEnemy;
```

These give us the camera that we can shoot the raycast from and the layer mask to identify if what we hit was an enemy or not.

The last variables we need are private for the purposes of the script:

```.cs
    private RaycastHit _rayHit;
    private bool _shooting, _readyToShoot, _reloading;
```

### Awake Function

```.cs
    private void Awake()
    {
        _bulletsLeft = magazineSize;
        _readyToShoot = true;
    }
```

In the awake function we need to set the amount of bullets that we currently have equal to the capacity of the magazine so we can start with the right amount of ammo.

We also need to set our `_readyToShoot` variable to true so we can be able to shoot.
