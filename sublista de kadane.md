Dada una lista de números enteros (positivos, negativos o cero), encuentra la sublista contigua cuya suma sea máxima y devuelve el valor de dicha suma.

Ejemplo
Entrada:
nums = [-2, 1, -3, 4, -1, 2, 1, -5, 4]

Salida:
6
(La sublista con suma máxima es [4, -1, 2, 1]).

```kotlin

fun maxSubarray(nums: List<Int>): Pair<Int, Int> {
    if (nums.isEmpty()) return Pair(-1, -1) // Si la lista está vacía, no hay sublista válida

    var maxSum = nums[0]   
    var currentSum = nums[0] 
    var start = 0 
    var end = 0 
    var tempStart = 0  

    for (i in 1 until nums.size) {
        if (nums[i] > currentSum + nums[i]) {
            currentSum = nums[i]
            tempStart = i
        } else {
            currentSum += nums[i]
        }

        if (currentSum > maxSum) {
            maxSum = currentSum
            start = tempStart
            end = i
        }
    }
    return Pair(start, end)
}

val nums = listOf(-2, 1, -3, 4, -1, 2, 1, -5, 4)
val (start, end) = maxSubarray(nums)
println("Mejor sublista está entre índices $start y $end: ${nums.subList(start, end + 1)}") 
// Output: Mejor sublista está entre índices 3 y 6: [4, -1, 2, 1]
