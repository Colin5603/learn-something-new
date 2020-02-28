# fast inverse square root #
- first we need to know how float number stored
- this method gives a very strong initial value for Newton's Method, making it converge quickly.

	float Q_rsqrt( float number )
	{
		long i;
		float x2, y;
		const float threehalfs = 1.5F;

		x2 = number * 0.5F;
		y  = number;
		i  = * ( long * ) &y;                       // evil floating point bit level hacking
		i  = 0x5f3759df - ( i >> 1 );               // what the fuck? 
		y  = * ( float * ) &i;
		y  = y * ( threehalfs - ( x2 * y * y ) );   // 1st iteration
	//	y  = y * ( threehalfs - ( x2 * y * y ) );   // 2nd iteration, this can be removed

		return y;
	}

Here ## magic number 0x5f3759df ##, for the rationale, see [fisr algorithm](https://en.wikipedia.org/wiki/Fast_inverse_square_root#Algorithm)
	
