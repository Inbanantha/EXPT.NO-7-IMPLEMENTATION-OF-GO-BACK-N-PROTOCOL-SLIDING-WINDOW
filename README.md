# EXPT.NO-8-IMPLEMENTATION-OF-GO-BACK-N-PROTOCOL-SLIDING-WINDOW
# AIM
To write and execute a program for Go-Back-N protocol.
# EQUIPMENTS REQUIRED
Personal Computer Turbo C Compiler
# PROCEDURE
1.	Connect two computers in Wired/Wireless LAN.
2.	Make sure that two computers are in one network and could able to ping each other.
3.	In the codeblocker open new c file and type the program.
4.	In the menu choose->Project->Properties->Project Build options->Linker settings->Add netproto and pthread.
5.	Execute the program in both server and client.
6.	Enter the IP address of the remote machine, port address of both local & remote machine and error rate.
7.	Choose the file and verify the go back protocol operation.

# PROGRAM
```
#include <stdio.h> 
#include <stdlib.h> 
#include <string.h> 
#define WINDOW_SIZE 4 
#define MAX_FRAME_LEN 100 
int main(void) 
{ 
int n; 
printf("SLIDING WINDOW PROTOCOL - GO BACK N ARQ\n"); 
printf("Enter the number of frames: "); 
if (scanf("%d", &n) != 1 || n <= 0) { 
printf("Invalid number of frames.\n"); 
return 1; 
} 
/* allocate array of strings (indexing frames from 1..n for convenience) */ 
char **frame = malloc((n + 1) * sizeof(char *)); 
if (!frame) 
{ 
perror("malloc"); 
return 1; 
} 
for (int i = 0; i <= n; ++i) frame[i] = NULL; 
for (int i = 1; i <= n; ++i) { 
frame[i] = malloc(MAX_FRAME_LEN); 
if (!frame[i]) { 
perror("malloc");
return 1; 
} 
printf("Content for frame %d: ", i); 
scanf("%99s", frame[i]); /* limit input to avoid overflow */ 
} 
int window_start = 1; 
int ack; 
while (window_start <= n) { 
int window_end = window_start + WINDOW_SIZE - 1; 
if (window_end > n) window_end = n; 
printf("\nSending frames %d to %d: ", window_start, window_end); 
for (int i = window_start; i <= window_end; ++i) printf("%d ", i); 
printf("\n"); 
printf("Enter ACK (0 = all frames in window ACKed, or enter frame number NOT 
ACKed): "); 
if (scanf("%d", &ack) != 1) { 
printf("Invalid input. Exiting.\n"); 
break; 
} 
if (ack == 0) { 
/* all frames in this window are acknowledged, slide window forward */ 
window_start = window_end + 1; 
printf("All frames in window acknowledged. Next window starts at %d\n", 
window_start); 
} else if (ack >= window_start && ack <= n) { 
/* go-back-n: resend from the first unacknowledged frame */ 
printf("No acknowledgement for frame %d. Resending from frame %d.\n", ack, ack); 
window_start = ack; 
} else { 
printf("Invalid frame number. Enter 0 or a frame number between %d and %d\n", 
window_start, n); 
}
} 
if (window_start > n) { 
printf("\nAll frames sent successfully.\n"); 
} 
/* free memory */ 
for (int i = 1; i <= n; ++i) free(frame[i]); 
free(frame); 
return 0; 
}
```
# OUTPUT

 <img width="1118" height="925" alt="Screenshot 2025-10-14 113225" src="https://github.com/user-attachments/assets/7f3ca784-5cea-4653-b2d4-25f3e4881b08" />





# RESULT: 
 Thus the Go-Back-N protocol-Sliding Window was implemented and the output is verified successfully.
