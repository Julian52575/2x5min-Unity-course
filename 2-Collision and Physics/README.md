## Physics

#### What you will learn:
- Which built-in systems exists for handling physics
- What component to use
- How to configure a game object's physics
- How to disable collision between objects

#### What you will avoid:
<img src="./chairsFail.gif" width="240"> <img src="./ratFail.gif" width="200">    

###### _Example of fails you will never encounter thanks to this lesson_

An image is worth a thousand words, so this page will contain a billion words within multiple gifs:

### Colliders vs Rigidbodies

![comparison](./Comparison.gif)
###### _Red objects have only a collider, blue only have a rigidbody and purple have both._

> [!TIP]
> All types of Collider allow collision detection, but do not influence the object's transform on their own.

> [!TIP]
> Rigidbodies determines how physics _(gravity and other objects)_ interract with the object's transform. 

------------
### Collider

![all colliders](./allColliders.png)
###### _All available colliders, trust your instinct on which one to use_

> [!NOTE]
> Parameters differs depending on the collider type.
> The most useful ones are:
> - `Is Trigger` _(this component will not be used for physics, but user scripts can use it to check collision)_
> - `Provides Contacts` _(store collision data to be accesed/used anytime)_
> - `Layer Overrides` _(see below)_
> - `Height`
> - `Radius` 

> [!TIP]
> You can use any type of collider with any game object.
> A cube could have a capsule collider if you need extra space for your hitbox.
> ![transCube](./cubeWithCapsuleCollider.gif)

-------------
### Rigidbody

![70 vs 1 mass](./Mass70vs!.gif)
###### _The ball's mass is now 70 but the mass of the step is still 1._

##### Tasks

[] Create a Sphere game object
[] Create other shapes

| [] Place the sphere on top of another object
| [] Play the scene
| 🔁 _repeat until bored_

> [!TIP]
> The only parameters worth worrying about are:
> - `Mass`
> - `Use Gravity`
> - `Constraints` to freeze any of the tranform's Position/Rotation 
> - `Layer Overrides` to include/exclude some other objects (see below)
> - `is Kinematic` (see below)

-----------------
### Ignore layers

Both Colliders and RigidBodies have a properties that allows you to configure interactions with different layers.
You can use it to disable collision between objects.

##### Tasks

[] `Add Layer...` and create a layer in one of the 26 spots available
[] Assign the layer to one of your object   

![layer](./layers.png)

[] Update the sphere's component to exclude the object's layer

![ignore reset](./IgnoreReset.gif)

> [!TIP]
> You can set either:
> - a custom layer on your step, and exclude it in one of the ball's component
> - a custom layer on your ball, and exclude it in one of the step's component
> - 2 custom layers (best) and exclude them in all gameobject's components

-------------------------------------------
### RigidBody Kinematic and script movement

> _in British English_
> _adjective_
> _**relating to the motion of bodies without reference to mass or force**, [...]_
###### https://www.collinsdictionary.com/dictionary/english/kinematic

Enabling kinematic disable gravity and other object's force.    
The object will only update its tranform through its scripts, but still cause updates to the other objects' transforms.

#### Tasks

[] Enable an object's `is Kinematic` RigidBody parameter
[] Create a new script
[] Write the `void FixedUpdate()` function that calls `GetComponent<Rigidbody>().MovePosition();`

```c#
void FixedUpdate()
{
    float speed = 2.0f;
    Rigidbody rb = GetComponent<Rigidbody>();
    Vector3 targetPosition = rb.position + new Vector3(0, -speed, 0) * Time.fixedDeltaTime;

    rb.MovePosition(targetPosition);
}
```

> [!CAUTION]
> Use `FixedUpdate()` instead of `Update()` to ensure physics runs at a stable framerate and look smooth.

![kinematic move](./kinematicFall.gif)

----------

**You are now a master of Unity's physics and saved yourself hours of work.**
[LET'S LEARN SOMETHING ELSE](./../README.md#Concepts)
