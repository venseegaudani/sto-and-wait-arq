#include<stdio.h>
#include<stdlib.h>
#include<time.h>
#include<unistd.h>
#define TIMEOUT 3
int main()
{
    int sender=0;
    int receiver=0;
    int ack=0;
    int seq=0;
    int num_packets=5;
    int t_start = 0;
    while (seq<num_packets)
    {
        printf("Sender: Sending Packet %d\n",seq);
        sleep(1);
         t_start= time(NULL);
        while (time(NULL) - t_start<TIMEOUT)
        {
            if(receiver==seq)
            {
                printf("Receiver:Received packet %d\n",receiver);
                ack=receiver;
                receiver++;
                break;
            }
        }
        if(ack==seq)
        {
            printf("Sender: Received acknowledgement %d\n",ack);
            seq++;
        }
        else{
            printf("Sender:Timeout on Packet %d",seq);
        }
    }
    printf("Transmission complete \n");
    return 0;
}



