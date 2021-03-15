using System;

namespace Solution
{
  public class TwiceAsOldSolution
  {
    public static int TwiceAsOld(int dadYears, int sonYears)
    {
      return Math.Abs(dadYears - sonYears * 2);
    }
  }
}