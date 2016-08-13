CryptoAccel
===========

Use the on-chip cryptographic accelerator for symmetric cyphers and one-way hash algorithms.

This software may only be used with as part of a programmable processing unit (e.g. a microprocessor, microcontroller, or digital signal processor) supplied directly or indirectly from Freescale.  See Freescale_License.txt for details.

AES
===

Perform an AES key expansion
----------------------------

    void   mmcau_aes_set_key (const unsigned char *key,
                              const int            key_size,
                              unsigned char       *key_sch)
    
          *key        pointer to input key (128, 192, 256 bits in length)
           key_size   key_size in bits (128, 192, 256)
          *key_sch    pointer to key schedule output (44, 52, 60 longwords)


Encrypt a single 16-byte block
------------------------------

    void   mmcau_aes_encrypt (const unsigned char *in,
                              const unsigned char *key_sch,
                              const int            nr,
                              unsigned char       *out)
    
          *in         pointer to 16-byte block of input plaintext
          *key_sch    pointer to key schedule (44, 52, 60 longwords)
           nr         number of AES rounds (10, 12, 14 = f(key_schedule))
          *out        pointer to 16-byte block of output ciphertext
    
          NOTE   Input and output blocks may overlap


Decrypt a single 16-byte block
------------------------------

    void   mmcau_aes_decrypt (const unsigned char *in,
                              const unsigned char *key_sch,
                              const int            nr,
                              unsigned char       *out)
    
          *in         pointer to 16-byte block of input chiphertext
          *key_sch    pointer to key schedule (44, 52, 60 longwords)
           nr         number of AES rounds (10, 12, 14 = f(key_schedule))
          *out        pointer to 16-byte block of output plaintext
    
          NOTE   Input and output blocks may overlap


DES
===

Checks key parity
-----------------

    int    mmcau_des_chk_parity (const unsigned char *key)
    
          *key        pointer to 64-bit DES key with parity bits
    
        return
          0           no error
         -1           parity error



Encrypt a single 8-byte block
-----------------------------

    void     mmcau_des_encrypt (const unsigned char *in,
                                const unsigned char *key,
                                unsigned char       *out)
    
          *in         pointer to 8-byte block of input plaintext
          *key        pointer to 64-bit DES key with parity bits
          *out        pointer to 8-byte block of output ciphertext
    
          NOTE   Input and output blocks may overlap


Decrypt a single 8-byte block
-----------------------------

    void   mmcau_des_decrypt (const unsigned char *in,
                              const unsigned char *key,
                              unsigned char       *out)
    
          *in         pointer to 8-byte block of input ciphertext
          *key        pointer to 64-bit DES key with parity bits
          *out        pointer to 8-byte block of output plaintext
    
          NOTE   Input and output blocks may overlap
   

MD5
===

Initialize the MD5 state variables
----------------------------------

    void   mmcau_md5_initialize_output (const unsigned char *md_state)
    
          *md_state   pointer to 120-bit block of md5 state variables:
                      a,b,c,d



Update MD5 state variables for one or more input message blocks
---------------------------------------------------------------

    void   mmcau_md5_hash_n (const unsigned char *msg_data,
                             const int            num_blks,
                             unsigned char       *md_state)
    
          *msg_data   pointer to start of input message data
           num_blks   number of 512-bit blocks to process
          *md_state   pointer to 128-bit block of MD5 state variables:
                      a,b,c,d


Update MD5 state variables for one or more input message blocks
----------------------------------------------------------------

    void   mmcau_md5_update (const unsigned char *msg_data,
                             const int            num_blks,
                             unsigned char       *md_state)
    
          *msg_data   pointer to start of input message data
           num_blks   number of 512-bit blocks to process
          *md_state   pointer to 128-bit block of MD5 state variables: 
                      a,b,c,d


Perform MD5 hash algorithm for a single input message block
-----------------------------------------------------------
    void   mmcau_md5_hash (const unsigned char *msg_data,
                           unsigned char       *md_state)
    
          *msg_data   pointer to start of input message data
          *md_state   pointer to 128-bit block of MD5 state variables:
                      a,b,c,d


SHA1
====

Initialize the SHA1 state variables
-----------------------------------

    void   mmcau_sha1_initialize_output (const unsigned int *sha1_state)
    
          *sha1_state pointer to 160-bit block of SHA1 state variables:
                      a,b,c,d,e


Perform the hash and generate SHA1 state variables for one or more input message blocks 
---------------------------------------------------------------------------------------

    void   mmcau_sha1_hash (const unsigned char *msg_data,
                            const int            num_blks,
                            unsigned int        *sha1_state)
    
          *msg_data   pointer to start of input message data
           num_blks   number of 512-bit blocks to process
          *sha1_state pointer to 160-bit block of SHA1 state variables:
                      a,b,c,d,e
    
          NOTE   Input message and state variable output blocks must not overlap



Updates SHA1 state variable for one or more input message blocks
-----------------------------------------------------------------

    void   mmcau_sha1_update (const unsigned char *msg_data,
                              const int            num_blks,
                              unsigned int        *sha1_state)
    
          *msg_data   pointer to start of input message data
           num_blks   number of 512-bit blocks to process
          *sha1_state pointer to 160-bit block of SHA1 state variables:
                      a,b,c,d,e


Perform SHA1 hash algorithm on a single input message block
-----------------------------------------------------------
    void   mmcau_sha1_update (const unsigned char *msg_data,
                              unsigned int        *sha1_state)
    
          *msg_data   pointer to start of input message data
          *sha1_state pointer to 160-bit block of SHA1 state variables:
                      a,b,c,d,e


SHA256
======

Initialize the hash output and checks the CAU hardware revision
---------------------------------------------------------------

    int    mmcau_sha256_initialize_output (const unsigned int *output)
    
          *output     pointer to 256-bit message digest output
    
    return
          0           no error -> CAU2 hardware present
         -1           error -> incorrect CAU hardware revision

Update SHA256 digest output for one or more message block arguments
-------------------------------------------------------------------

    void   mmcau_sha256_hash_n (const unsigned char *input,
                                int                  num_blks,
                                const unsigned int  *output)
    
          *input      pointer to start of input message
           input      number of 512-bit blocks to process
          *output     pointer to 256-bit message digest output
    
          NOTE   Input message and digest output blocks must not overlap
 


Update SHA256 state variables for one or more input message blocks
------------------------------------------------------------------

    void   mmcau_sha256_update (const unsigned char *input,
                                const int            num_blks,
                                unsigned int        *output)
    
          *input      pointer to start of input message data
           num_blks   number of 512-bit blocks to process
          *output     pointer to 256-bit message digest output



Perform SHA256 hash algorithm for a single input message block
--------------------------------------------------------------

    void   mmcau_sha256_hash (const unsigned char *input,
                              unsigned int        *output)
    
          *input      pointer to start of input message data
          *output     pointer to 256-bit message digest output


