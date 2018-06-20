
# Using GMP(GNU Multiplple Precision) Library with C/C++

### Code compilation
```
gcc -o progname progname.c -lgmp          //for C code
g++ -o progname progname.c -lgmpxx -lgmp  //for C++ code
```
### Including the gmp library
```
#include <gmp.h>
```

### Initalizing an integer
```
int x = 31415926;
mpz_t pie;
```

### Assignement functions
```
mpz_init(pie);
mpz_set_ui(pie,x);
or
mpz_init_set_ui(pie,x);   //initialize and assign a value
mpz_init_set_str(pie, "31415926..", 10); //mpz_init_str(mpz_t pie,str, base);

mpz_init_set_ui(mpz_t t, usigned long int l);
mpz_init_set_si(mpz_t t, signed long int l);
mpz_init_set_d(mpz_t t, double l);
```

### Operations
```
mpz_add(ans,a,b);   //ans = a+b;
mpz_sub(ans,a,b);
mpz_mul(ans,a,b);
```

### Conversions
```
unsigned long int mpz_get_ui (const mpz_t n);
signed long int mpz_get_si (const mpz_t n);
double mpz_get_si (const mpz_t n);
char * mpz_get_str(char *str, int base, const mpz_t n);
```

### Output 
```
gmp_printf("%Zd ", ans)   //outputs a mpz_t variable
mpz_out_str(stdout, 10, n); //mpz_out_str(str,base, mpz_t n);

```

### Clear out the variables after done for memory management
```
mpz_clear(n);
```

