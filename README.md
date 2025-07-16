import scala.io.StdIn 

object MathFunctionsBinarySearchWithUserInput {

  def calculateSquareRootBinarySearch(n: Double, tolerance: Double = 1e-9, maxIterations: Int = 100): Double = {
    if (n < 0) {
      throw new IllegalArgumentException("Karekök sadece negatif olmayan sayılar için hesaplanabilir.")
    }
    if (n == 0) {
      return 0.0
    }

    var low = 0.0
    var high = if (n < 1.0) 1.0 else n
    var result = 0.0

    for (i <- 1 to maxIterations) {
      val mid = low + (high - low) / 2.0
      val square = mid * mid

      if (math.abs(square - n) < tolerance) {
        return mid
      }

      if (square < n) {
        low = mid
      } else {
        high = mid
      }
      result = mid
    }

    println(s"Uyarı: Karekök hesaplaması maksimum iterasyon sayısına ($maxIterations) ulaştı. Yaklaşık değer dönülüyor.")
    result
  }

  def main(args: Array[String]): Unit = {
    var inputIsValid = false
    var numberToCalculate: Double = 0.0

   
    while (!inputIsValid) {
      print("Karekökünü hesaplamak istediğiniz pozitif bir sayı girin: ")
      try {
        val input = StdIn.readLine()
        numberToCalculate = input.toDouble

        if (numberToCalculate < 0) {
          println("Hata: Lütfen negatif olmayan bir sayı girin.")
        } else {
          inputIsValid = true
        }
      } catch {
        case _: NumberFormatException =>
          println("Hata: Geçersiz giriş. Lütfen bir sayı girin.")
        case e: Exception =>
          println(s"Beklenmeyen bir hata oluştu: ${e.getMessage}")
      }
    }

    
    try {
      val result = calculateSquareRootBinarySearch(numberToCalculate)
      println(s"Girilen sayının ($numberToCalculate) karekökü: $result")
    } catch {
      case e: IllegalArgumentException =>
        println(s"Hata: ${e.getMessage}")
      case e: Exception =>
        println(s"Karekök hesaplanırken bir hata oluştu: ${e.getMessage}")
    }
  }
}
