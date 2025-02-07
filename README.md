
# Factor integers in C
Basic C99 **factorization** software. There is also a [Quadratic Sieve](https://github.com/michel-leonard/C-Quadratic-Sieve) for larger numbers.

This ~100 lines C software :
* uses a **Miller–Rabin** primality test
* uses a **Pollard's rho** algorithm

# Example output

```c
  358205873110913227 =    380003149 * 942639223    took 0.01s
  195482582293315223 =    242470939 * 806210357    took 0.0021s
  107179818338278057 =    139812461 * 766597037    took 0.0023s
   44636597321924407 =    182540669 * 244529603    took 0s
  747503348409771887 =    865588487 * 863578201    took 0.016s

// GCC 128-bit extension available output :
170141183460469231731687303715506697937 =
13602473 * 230287853 * 54315095311400476747373 took 0.137699s

2139508543525359760856377898747 = 18122728927937 * 118056643236947131 took 17.2946s
2080913777018885818418638213057 = 283954641807703 * 7328331608778919 took 40.8842s
```

factor(n, array)
------------

**parameter 1:** *positive_number* N\
**parameter 2:** *positive_number\** array

Fill the second parameter array with the prime factors of N.

```c
// 64-bit source code is here.

#include <stdio.h>

int main(void) {
    // allocate memory for 64 factors.
    positive_number *array = calloc(64, sizeof(positive_number));

    positive_number n = 7806418495977353572 ;

    size_t n_factors = factor(n, array) - array ;
    printf("There are %zu factors of %llu : \n", n_factors, n);
    for(int i = 0; array[i]; ++i)
        printf("- %llu\n", array[i]);
    free(array);
}
```
So you displayed the factors of `n` :
```
There are 4 factors of 7806418495977353572 : 
- 2
- 2
- 120317621
- 16220438933
```
Compilation
--
The software should be executable on many platforms like Windows, Debian, Ubuntu, Linux, ...\
You can rename `main-64-bits.c` or `main-128-bits.c` to `primes.c` then compile + execute :
```sh
gcc -O3 -std=c99 -Wall -pedantic primes.c ;
./a.out ;
```
You can normally [try it online](https://tio.run/##rVlbc6M6En7Pr9DJVmZMbCdICBDLJFP7A/Zla9@yUy6McUyNDSnAkzOX/PbZlsD050tqz8O6ZmxF6m715etuIfL5c57//v23ssq3@1UhPrXdalsu7zaPVzjXlNWznbvqvr8Uq2ItFot9WXVSmUUnXuq27MpvxaLa75ZFk15dtV3Wlfnpgtjtt135si1zWq2rxa5e7bf15JQqm50xLmcir6u2O5dYrzzx80rQ53SpKVrxIPyZ6HYvqaNY142YLMXNg2VLRUb/xAchxWexFI9uUswd22f3Pe@n/m5l2L@nD0Tn/srEI9HLmZiQbNpk6TH/krjtLHIvLS9Ner0eTdHtm8rJvHGqXL2NLiOnirJdvDTlrjjzTDVz61/fMznrDbbemonVTBQzsZ6J59RxbYi5379ci8mkEg9kgme/aUxu8LyDYm5JMW0lPgkdRUmiiP7@XqwzioSLR/HnS@Pc2u6y7VY4rVvyyqZsxbasCjKFhO7qb9lyW3h3TiJ4YDLsTF8Tt0vkiVuhlZgK/0/lm38oYxT59pFUuhGBLz58GLRJxK9fdngjYjtpB1KOo2Ac8WpyGKlxVSWjwCSSo8RgFBSM7Hqc0yO7HlfDcS4ct4lGjigetwl9zfvEI0U88scjvxnnzDiXsDk@W@uzuT5vJaUxvJf0E/YT0ysWGID7YJbZNA9Dpg15RxWFEcdFRrxNxAJjiA0LNCwwgSHTguUJR03rULGNihGgIMhso1IAAiZgGxWHWYUwZBujRIKNim1UEUvhwKqYN2cblQEIjsPAH2mD3pIemXECOwYcvIDBHQBkOXiBhuGoXcBgDRitAYCUgi4VbMkhCzhkAdsQMEADjpNmhGoGn@Y81IqNlCaMIQN1AOnG@caB0pCFbJoOeXdOP81B0mAlgUFDMmo2TRsWw2jUyUgQcsaFbFqoJA@ZQLOViiqoz44NoYCw5iGrGzKmQsZUyJgKWdMwgRrEGRJEUvlsZcRBiRhuEYMqkjDLtYzjEWkYMptmx2oVabAyYrxFUB2xPDIBmxYxviIOQuzDkK0MKSkjLKzjPjFnf8xIihlJMRsRc8rHHI@YNY0j2DKJQ0iSGEo4ByXmdDAMFMN1yigYcsFnpQ30qNgPEih3ho0w7GPDmht2t2FQGfax4ZJkoN0YjqVRFEy2MmHMJGxEwu5OuMImXIgSxkzCmE9Y6QTyMtHKQF4mDPyENU9Y3YTRkWB/hIbnQ8fzJcxjBfIjhRiiroodFgRAS/ShJ/rQFP0Ix8AbAb3BXp346rhbgwBogz5YiH3/qL3DoUcqoFFAE4LlAVVCSFhaBCbQXnIoJHZsaWBDUFbBGUXhoUOC5ToJY8gjCZ1bQr8mQ0AYHFAUhECFMI6BBk4aQ@/tN6cqhAcIWgRCCIECtwdgVQAhgPZNZymWEyigVzG2PBXg5gGAJoATE/RfGYDbgwTOZhB/DR7UcMDTUEqUHwbagNuhzUqNhz4NAgDhGjCiwe0aMKINjgPovIRRPClCw5Xa4IkTNknw@AnnT7A2BIyEGuY1WK4Jr4j2ECwJwZIQQgDdl8ZAY4AXMAJtVkZwJlehMUen8gjiBl1YQu@VEQAognhGkAVRCGM8eOOBJzZhiBUugmoUgasjtATcHoOyMSgVQwigycoYjj6BHyof3R4DsGIIQQwhiCGHY3A1dFgaw1MEuN3AEToI6LiPRQZ6rTQAGgNKGUhHA1gwgAUDqQl9lcZwAgvpKIN5bkDjBDSG5koPQfDoE@ATEcxD5UsgNZOYU41O8hGecmkRmAw@VIHgo4ctfqzxudpRaZcw5occHyocZVqErZwWQRg8dfkhCI5wDDTw@OTD85NvYHODj4Z@aHzcHCyRoD08DitokQoeiBU8ESsJz4hSAy8Z4f2/Pkf3VQ8ip/@VmNsbp4294knFHzRvb05Se3XV30VNpxvkS8XX@Tw93BSN0889/zO5qC1/FPX69JKJRE4m@SZrbr0Pmff0PJ1@IZYmq1YT0ste/9hxvRM9Od/prOp@hxWRF/RfiqnIyDP5TKyt/qldunkQa88FaW3HKy8ddLaf1025LSzVo3A@XtsBrI/irTyZ0s@nB7F0v58ezintgvNNKizT5cvHlbsoqzyr5AdyplXtfepioPZgL3tDthou0/K66spqX5xoUpLATSrK@dzKX4k/KKR/RamzXSzjeE3n96tveKco3V3i6b3gOsu7ulm81s3XoplcvkmtDlCxsFh07i5xLu3d5YNQIr1432hvGYdI9wDprxx7YgtaF/Cq/5vw8fPInOk0s25bejxtP4SwDQkjJHyv943oyl1R7zuxKRqS/bopKjFxfJKiTmntCfJwVtUdEZCCr/Rdr0X3Wt8dSbV65tYaB5VZf1XK7n0bR/m7UcndtWp1CrPp1C6IW5umFJ9q5tBf9ajPCcIr8Zl@58JeBtsbYgp9j/6iz4Siz4pDJrwd8oCIfjmiBwb3EOa1C7O9ii23W0Gmi2cKSyWypsm@i9ey2/R3sUPkW@uSyt1ik2W0TkzLQvwomlp0RbMrq6wrVndnuLkd@C9dRJ/Rur3fvZme2UQdoNWKERF8v@wdhauXNp32nqxcvo8ExbYtBkZ3e3yMn7FqVvbieAg1TUxp4t5d1T/akpDRpsvUwTu7TAOBPkB2SS5Z2nhUp7u6zLGlqXfYciYGf8yHoKRn5Ltil798n/TLU9EOLDOSc/tecfYuyBkEPBDfdPQtfk7c14PMOfHcBmvl@P6BXK@N5@78hzgSjv5J6Cma@b@yZVkRetquvTuT8j9DeBTKnxf5s9Gbh8JV9f3naFLkWfWxs2jOM9Jr1YM/6@F/WbHeX2OoskOo0ovUBAhCyPna29Xlv3rPniPS9uxq6NngGjVzOOUMH5K/gt53e9DYF0dV4AAsKgVH7@/K@vj1Xda2RdO513fkvpem/lauyFNWLeoFVDfKosqpuHbZ14Jc17/to5q6Gjeyj8bzZdmJfdWWzxUxl1VXPNv2jy8C1029W/TsCztDHO3QbuyJQtzS2iFxkG94VXd0erG06bBiv2@F9AnfdpocNxcf/Y9nr9MOVXE0sastEKruXf0Ju8OLt17Brj7THxWlLBjbJLC1T9r/kp6Ztcvar66LpkeNtX9BJ1wbWg1LXWNLAZWAa/8aT3FOhH2VaH/vhUrdqP8eYHN6wnOljBQlrFkqzzYlv@/j1HmW6Wnlsp1xMmmf5vPll8GvtrOS4Okp7tunpT0MXvtSBZoekE1y/bRy91Jfjgkz1/vvaeFSix0inKXC9U6qg7v6WzGx5YtcQk7I6SBx257ulPU72WJNKSl978L5p4eAjfguK6vJt7oc3w8TLqhC1NTTC7tl3Xx3ikT60CTvLnauMflyxz2J9Ozd4pxeXRRha9/F1LhO/sJHJte26iOEqsWhr49VrHqn4Tj4ryfX/7bnJ1qhw8aPPR4Lblo6lvynup6xVKoE52lQwVPJxL2l7p8k3GZP5RcbzJKb@GHfOW3gpF8QeWAdJTdFMTnU4rer37//Cw) with [DigitalOcean](https://www.digitalocean.com/) 128-bits, Thank You.

Shortest link to this page : [bit.ly/C-RHO](http://bit.ly/C-RHO)

