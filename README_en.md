# 8dot8 CTF

[Partner in crime: Federico Videla](https://github.com/acidobinario)

Third place, first place next year >:)

## hHIS

If we go to the host on a browser we see:

![Host in browser](./images/Screenshot%20at%202022-10-21%2023-40-20.png)

It tells us we've answered incorrectly, even though we haven't interacted with the app. However if we go to the host using `netcat` we get:

![Host in netcat](./images/Screenshot%20at%202022-10-21%2023-44-44.png)

Much better, now It's an interactive app. Let's focus on `Qbun wifil qum Muhncuai'm qbcny bilmy?`. Rotation ciphers are easy to recognize:

![https://dcode.fr](./images/Screenshot%20at%202022-10-21%2023-53-18.png)

We input the answer (white) and we're prompted with a second question:

![Tai ymzk yqynqde oaybaeqp ftq Rqxxaietub ar ftq Duzs?](./images/Screenshot%20at%202022-10-21%2023-55-35.png)

After a quick search we get out answer:

![Nine members](./images/Screenshot%20at%202022-10-22%2000-05-01.png)

After that, we get a third question:

![Last question](./images/Screenshot%20at%202022-10-22%2000-07-30.png)

Honestly, no clue what this means:

![WHAT???](./images/Screenshot%20at%202022-10-22%2000-10-37.png)

So I just hit enter:

![haha](./images/Screenshot%20at%202022-10-22%2000-13-08.png)

## Broken Jar

> Federico and I both agreed this should've been the "hard" challenge, it tooks us almost 5 hours to solve it.

If we download the binary and execute it, we see a prompt, if we try to log in as "Superb Admin", it returns an error and segmentation fault.

![Segmentation Fault](./images/Screenshot%20at%202022-10-22%2000-23-55.png)

We open the binary in ghidra and check the function `superb_admin`:

![Superb_admin](./images/wd8yj6.png)

As we can see, if we manage to set the user in `idx` 0 to `root` we'll get a shell. Let's try it:

![hehe](./images/Screenshot%20at%202022-10-22%2000-34-31.png)

Let's check the function `add_user`:

![add_user](./images/dwqmib.png)

We can see it does a `strcmp` which will not allow us to set the user as root, so, what do we do?

Now, I have to admit we remained stuck on this part of the challenge for a few hours, we both don't have much experience with binary RE, so I started asking around for some help. Luckily, someone came to our rescue and pointed out this challenge was very similar to the one given on this [writeup](https://infosecwriteups.com/arming-the-use-after-free-bc174a26c5f4)

![i lol'd](./images/Screenshot%20at%202022-10-22%2000-53-20.png)

Let's try it on our binary:

![1](./images/Screenshot%20at%202022-10-22%2000-58-44.png)

![2](./images/Screenshot%20at%202022-10-22%2000-59-42.png)

It worked! Let's try it on the server:

![got the flag](./images/Screenshot%20at%202022-10-22%2001-04-05.png)

## One Man Chance

> This challenge was much easier than the [previous one](#broken-jar), It should've been the "medium" one

If we check the given code we can notice two things:

![code](./images/Screenshot%20at%202022-10-22%2001-20-24.png)

1. We have key `a`: `9123891238912389`
2. Key `b` is a "random" number between `0` and `99999`

Which makes decryption really simple:

![decryption](./images/Screenshot%20at%202022-10-22%2001-25-27.png)

We get the encrypted flag from the server:

![Encrypted flag](./images/Screenshot%20at%202022-10-22%2001-27-41.png)

And using our bruteforcing code, we get:

![Decrypted flag](./images/Screenshot%20at%202022-10-22%2001-29-43.png)
