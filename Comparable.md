**Comparable Overview**

The Java `Comparable` is used when you want to sort a custom class you have just made or when you want to sort an already established datatype (like a `String`) in a custom way. When using the `Comparable` it is important to note that when comparing object a to object b, if a negative number is returned, a comes first, and if a positive number is returned, b comes first.

**Use in the sorting of custom classes**

When you create a custom class you will use the `implements` to include `Comparable`

    // We will create the custom class car, which sorts cars by their respective speed, if the speed is the same then
    // We will sort by coolness factor.
    class Car implements Comparable<Car> {

	private int speed, coolness;
	
        public Car(int s, int c) {

        speed = s; coolness = c;

        }

	@Override
	public int compareTo(Car o) {
		if (this.speed < o.speed) {
			return -1;
		}else if (this.speed > o.speed) {
			return 1;
		}else {
			return this.coolness - o.coolness;
		}
    	}
	
    }