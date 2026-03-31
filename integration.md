ack get sys/Shell
ack get sys/Pipe

final class Error<T> {
    public:
        enum types;
        string type
        string msg;
        T onBoard;
}

#include "sys/Shell.h"
#include "sys/Pipe.h"

class OnBoard
{
    // TODO pass anything you want
}


int runner()
{
    sleep(10);
}

int time_out()
{
    //TODO
}


int argumentStyle(int i)
{
    return i++
}

int main()
{
    Shell s;
    s.env["test"] = "keke";
    print(s.prompt("echo $test"));
    print(s.env["$?"]);

    int[] arr = [1, 2, 3];
    if (arr.in(1, 2, 3))
        print("viva l'algerie");

    Pipe p;
    p.runner = runner;
    p.timeout(10, time_out); // not triggered
    p.execute();
    sleep(10);
    p.wait(); // no effect

    p.timeout(5, time_out); // triggered
    p.execute();
    sleep(10);
    p.wait(); // no effect

    try
    {
        p.timeout(null); // not triggered
        p.execute(runner).wait();
        Error<OnBoard> err("i just wanna trigger something");
        throw err;
    }
    catch // no need for var here... Error is a final class. The scope give access to error
    {
        print(error)
        if (error.type == Error::types::runtime)
            print("system error :\n" + error)
        else if (error.type == "my error")
            print("personnal error :\n" + error)
    }

    int i = 1;
    argumentStyle(i);
    print(i); // 2

    i = 1;
    int j = argumentStyle(i.copy());
    print(i); // 1
    print(j); // 2
    print(&j); //adress pointer

    int k = new Integer(10); // the formater could give k a special color as its on the heap. But im not sure it could be tracked outside of the scope.
    int l = new Integer(2); // the formater could give l a special color as its on the heap. But im not sure it could be tracked outside of the scope.

    i = k; // ok, i = 10
    i = &k; // ok, i = the k adress
    &i = &k; // ok, i = 10
    k = 5; // ok, i = 5
    l = k; // ok, l = 10
    l = &k; // ok, l = the k adress
    &l = &k; // maybe it is possible to trigger a compilation error here as we loose the l reference



    return 0;
}

