CSCI368/CSCI968 - (Advanced) Network Security Spring 2024 Assignment 1 (10 Marks, Weight 15%) Submission Due: 21 Aug 2024 23:30 Objective On completion of this assignment, you should be able to use some basic cryptographic techniques to secure remote communications. Programing Task Write (Java/C++/Python) UDP programs to allow two parties to perform authentication and establish a secure communication channel. For simplicity, let us call the programs “Host” and “Client”, which are executed by Alice and Bob, respectively.Alice and Bob share a common password PW, which contains 8 alphanumeric characters. Alice also has a public and privacy key pair (pk, sk) for the RSA encryption scheme. They want to establish a secure communication channel that can provide data confidentiality and integrity. This will be done via the following steps: (1) perform an authentication and key establishment protocol to establish a fresh secret key; and (2) use the established secret key to secure the real communication. Step 1 is done via the following authentication and key establishment protocol: 1: B → A: Bob, NB 2: A → B: Alice, pk, NA 3: B → A: C1 = PKE pk(PW, K) Alice decrypts C1 using sk to get PW and K, and then verifies PW. Alice sends either “Connection Okay” or “Connection Failed” to Bob to indicate whether the connection is successful or not. 4: A → B: Connection Okay/FailedIn the above protocol, NB and NA denote two 128-bit random strings chosen by Bob and Alice, respectively, and PKE denotes the RSA encryption. K is a 128-bit random secret key selected by Bob. Alice and Bob then compute the shared secret key as ssk = H(K,NB,NA) where H denotes the SHA-1 hash algorithm. After establishing the secret session key, step 2 is done as follows:

      whenever Alice wants to   send a message m   to   Bob,   Alice   first   computes   an   integrity   check   value   h = H(ssk, m), and then computes C =   SKEssk(m||h)   and   sends   C to   Bob;

  upon   receiving   a   ciphertext   C,   Bob   first   runs the   decryption   algorithm   to   obtain   m||h.   After that,   Bob   computes   h   ’ =   H(ssk,   m)   and   checks   if h   =   h   ’.   If the   equation   holds,   then   Bob   accepts   m;   otherwise, Bob rejects the ciphertext;

  the same operations are performed when   Bob sends   a message   to   Alice.

The SKE in step 2 denotes the RC4 stream cipher. Implementation guidelines • Place Host and Client in two separate directories: Alice and Bob. Alice also stores a password file in her directory. The password file contains all the user records, e.g., (Bob, H(PW)). • Generate a public and private key pair for Alice, and store the generated public and private key pair in a key file under Alice’s directory. Store the fingerprint of Alice’spublic key (i.e., H(pk)) in Bob’s directory. This step is done u代 写CSCI368/CSCI968 - (Advanced) Network Security Spring 2024 Assignment 1C/C++ 代做程序编程语言sing a separate key_setup program. • Alice executes Host.

         Host is running   and   listening   to   the   opened   port   (you   need   to    select   a port   (e.g.,   5555)   for   Host).

• Bob executes Client that uses a different port number (e.g., 3333).

         Client asks   for   input   (username   and PW)   from   Bob   via   keyboard.

     Client sends the   first message   in   the   authentication protocol   to   Host.

     Upon   receiving the second   message from Host, Client checks if   the   received   pk   matches the   stored   fingerprint   of   the   Host.   If   they   don’t   match,   Client   terminates   the    connection;   otherwise, carry   on.

• Alice and Bob complete the authentication and key establishment protocol. • If Alice cannot successfully authenticate Bob, then Alice sends “Connection Failed” to Bob and wait for a new connection. Bob quits the program after receiving the message from Alice. • If the connection is successfully established,

         Either   Alice or Bob can send a   message encrypted and authenticated by the session key ssk.   They   type   the   message   on   their   own   terminal.   The   message   is   processed   by   their   code   according to step 2   given   above.

     A received message   is printed   on   the   screen    if   decryption   is    successful. Otherwise,   print   “Decryption   Error” on   the   screen.

     To   close   the   connection,   Bob   should type   “exit”   .

You can choose to use existing libraries or open source code to implement UDP sockets, RSA, RC4 and SHA-1. You should provide a reference if you use any downloaded code. How to run? Your programs should run according to the protocol. Host and Client should be executed on two different terminals. For convenience of marking, please use the local IP: 127.0.0.1 for the submitted version. For simplicity, there is no GUI required in this assignment. That is, messages are simply typed on one terminal and printed on the receiver’sterminal. Mark distribution:

      RSA key generation and   storage:   1 mark

  Authentication and Key Establishment (Step   1): 4 marks

  Data Encryption/Decryption (Step 2): 4 marks

  Proper and clear message display:   1 mark

Note: code that cannot be compiled or executed will receive a zero mark. Files to be submitted: All source codes (Do not submit any executable). A readme file (text/ACSII only): instructions about how to compile and run your code. Submission Compress all the files to be submitted into a zip file and submit it via the submission link provided in the Moodle site. Late Submission: Penalty is 25% deduction per day (including weekends) unless Academic Consideration is granted. Plagiarism A plagiarised assignment will receive a zero mark and be penalised according to the university rules. Plagiarism detection software will be used.

      Xujun Coding 📧 xujuncoding@gmail.com
