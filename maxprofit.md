Given a list of numbers and they represent the prices of a stock from the morning to evening of a trading day
[2, 5, 2, 7, 1, 2, 9]. Please write a method which returns the buy and sell indices to maximize the profit.
In this case, the method should return 4 and 6. 4 is the buy index and 6 is the sell index. Please note, we only want to buy and sell once.

```kotlin
fun maxProfit(prices: List<Int>): Pair<Int, Int>? {
    if (prices.size < 2) return null // Necesitamos al menos 2 precios

    var minIndex = 0  // Índice del precio mínimo encontrado
    var maxProfit = 0 // Máxima ganancia encontrada
    var buyIndex = 0  // Índice de compra óptimo
    var sellIndex = 0 // Índice de venta óptimo

    for (i in 1 until prices.size) {
        val profit = prices[i] - prices[minIndex]

        if (profit > maxProfit) {
            maxProfit = profit
            buyIndex = minIndex
            sellIndex = i
        }

        if (prices[i] < prices[minIndex]) {
            minIndex = i // Actualizamos el precio mínimo
        }
    }

    return if (maxProfit > 0) Pair(buyIndex, sellIndex) else null
}

fun main() {
    val prices = listOf(2, 5, 2, 7, 1, 2, 9)
    val result = maxProfit(prices)
    println(result)
}
