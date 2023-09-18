# GodotCoroutineslikeUnity
C# Coroutines in Godot game engine just like in Unity

1. Add PeakyCoroutine.cs somewhere in your project

2. Use like this...
    ```C#
    public override void _Ready()
    {
        Coroutine.Run(TestCoroutine(3f), this);
    }

    IEnumerator TestCoroutine(float waittime)
    {
        GD.Print("Start " + Time.GetTicksMsec());
        yield return new WaitForSeconds(1f);
        GD.Print("WaitedOneSecond " + Time.GetTicksMsec());
        yield return new WaitForSeconds(1f);
        GD.Print("WaitedAnotherSecond " + Time.GetTicksMsec());

        for (int i = 0; i < 20; i++)
        {
            yield return new WaitOneFrame();
            GD.Print("Waited One frame " + Time.GetTicksMsec());
        }

        yield return TestSubCoroutine(waittime);

        GD.Print("Final line from parent coroutine");
    }

    IEnumerator TestSubCoroutine(float waittime)
    {
        GD.Print("start sub routine " + Time.GetTicksMsec());
        yield return new WaitForSeconds(waittime);
        GD.Print("end sub routine " + Time.GetTicksMsec());
    }
    ```
I wanted to replicate the following features..
* Coroutines with pararmaters.
* Yield until next frame.
* Yield for certain amount of time in seconds.
* Yield another coroutine.
