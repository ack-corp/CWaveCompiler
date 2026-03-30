ack get sys/Shell

#include "sys/Shell.h"

int main()
{
    Shell s;
    s.env["test"] = "keke";
    print(s.prompt("echo $test"));
    print(s.env["$?"]);

    arr = [1, 2, 3];
    if (arr.in(1, 2, 3))
        print("viva l'algerie");

    return 0;
}