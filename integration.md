ack get sys/Shell

#include "sys/Shell"

int main()
{
    Shell s;
    s.env["test"] = "keke";
    print(s.prompt("echo $test"));
    print(s.env["$?"]);
    return 0;
}
