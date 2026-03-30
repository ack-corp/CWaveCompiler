ack get sys/Shell
ack get sys/Pipe

#include "sys/Shell.h"

int runner()
{
    sleep(10);
}

int time_out()
{
    //TODO
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

    p.timeout(null); // not triggered
    p.execute(runner).wait();

    return 0;
}