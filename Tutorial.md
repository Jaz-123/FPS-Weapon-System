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

In the awake function we need to set the `_bulletsLeft` equal to the `magazineSize` so we can start with the right amount of ammo.

We also need to set our `_readyToShoot` variable to true so we can be able to shoot.

### Update Function

```.cs
    private void Update()
    {
        MyInput();
    }
```

In the update function we are only calling the input function as all of the logic is happening in there.

### Input Function

```.cs
    private void MyInput()
    {
        _shooting = allowButtonHold ? Input.GetKey(KeyCode.Mouse0) : Input.GetKeyDown(KeyCode.Mouse0);

        if (Input.GetKeyDown(KeyCode.R) && _bulletsLeft < magazineSize && !_reloading) Reload();

        //Shooting mechanics
        if (_readyToShoot && _shooting && !_reloading && _bulletsLeft > 0){
            _bulletsShot = bulletsPerTap;
            Shoot();
        }
    }
```

In this function we are using an alternate if statement to check wether or not the player is holding down the shoot key and we store this as a bool `_shooting`.

Next we check if the player presses the R key to reload, we call the `Reload()` function if the player presses the key and the current amount of bullets is less than the size of the magazine and is also not already reloading.

The last statement checks if the player is allowed to shoot and if the `_shooting` variable is true as well as if we are not reloading and have bullets left in the magazine.
