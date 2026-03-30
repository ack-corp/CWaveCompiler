ack get sys/Shell

#include "sys/Shell"

int main()
{
    Shell s;
    s.env["test"] = "keke";
    printf(s.prompt("echo $test"));
    printf(s.env["$?"]);
    return 0;
}
