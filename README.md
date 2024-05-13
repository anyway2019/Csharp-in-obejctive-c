# Csharp-in-Obejctive-C

some csharp api implemention in objective-c.

### Guid

- #### Guid.ToByteArray()

  ```c#
    var guid = new Guid("fc9884a2-06c0-4b6e-9e00-d811f84a83ff");
    byte[] bytes = guid.ToByteArray();
    for (int i = 0; i < bytes.Length; i++)
    {
        Console.WriteLine(bytes[i]);
    }
  ```

  ```objective-c
    NSString *guidString = @"fc9884a2-06c0-4b6e-9e00-d811f84a83ff";
    NSUUID *uuid = [[NSUUID alloc] initWithUUIDString:guidString];
    uuid_t uuidBytes;
    [uuid getUUIDBytes:uuidBytes];

    //guid byte array in C# differs with uuid in oc,so here need alter array sort
    uint8_t temp = uuidBytes[0];
    uuidBytes[0] = uuidBytes[1];
    uuidBytes[1] = temp;
    temp = uuidBytes[2];
    uuidBytes[2] = uuidBytes[3];
    uuidBytes[3] = temp;
    temp = uuidBytes[4];
    uuidBytes[4] = uuidBytes[5];
    uuidBytes[5] = temp;
    temp = uuidBytes[6];
    uuidBytes[6] = uuidBytes[7];
    uuidBytes[7] = temp;

    //convert uuid_t to NSData
    NSData *data = [NSData dataWithBytes:uuidBytes length:sizeof(uuidBytes)];

    //print byte array to unsigned int
    const uint8_t *ubytes = (const uint8_t *)data.bytes;
    for (NSUInteger i = 0; i < ubytes.length; i++) {
        NSLog(@"%u", ubytes[i]);
    }
  ```

### double

- #### double.IsInfinity() and double.IsNaN()
  c#:
  ```c#
  if(double.IsInfinity(x) || double.IsNaN(x)){
    x = 0;
  }
  ```
  objective-c:
  ```objective-c
  if (isnan(x) || isinf(x)) {
    x = 0;
  }
  ```

### string
- #### string format
  ```c#
    var uuid = "2AD1";
    var str = $"0000{ uuid }-0000-1000-8000-00805F9B34FB";
  ```

  ```objective-c
    NSString *str = [NSString stringWithFormat:@"0000%@-0000-1000-8000-00805F9B34FB",@"2AD1"];
  ```

### Enum
- #### Flags
  ```c#
  [Flags]
  public enum RowerDataFlag
  {
      MoreData = 1,
      AverageStrokeRate = 2,
      TotalDistance = 4,
      InstantaneousPace = 8,
      AveragePace = 16,
      InstantPower = 32,
      AveragePower = 64,
      ResistanceLevel = 128,
      ExpendedEnergy = 256,
      HeartRate = 512,
      MetabolicEquivalent = 1024,
      ElapsedTime = 2048,
      RemainingTime = 4096,
      SingleEnergy = 8192,
      Pull = 16384,
      ThinkDragFactor = 32768
  }

  RowerDataFlag flags = 465;
  if(flags.HasFlag(RowerDataFlag.MoreData)){
    Console.WriteLine("MoreData");
  }

  if(flags.HasFlag(RowerDataFlag.TotalDistance)){
    Console.WriteLine("TotalDistance");
  }

  if(flags.HasFlag(RowerDataFlag.AveragePower)){
    Console.WriteLine("AveragePower");
  }
  ```
  ```objective-c

  @interface RowerDataFlag : NSObject

  @property (class, nonatomic, assign, readonly) int moreData;
  @property (class, nonatomic, assign, readonly) int averageStrokeRate;
  @property (class, nonatomic, assign, readonly) int totalDistance;
  @property (class, nonatomic, assign, readonly) int instantaneousPace;
  @property (class, nonatomic, assign, readonly) int averagePace;
  @property (class, nonatomic, assign, readonly) int instantPower;
  @property (class, nonatomic, assign, readonly) int averagePower;
  @property (class, nonatomic, assign, readonly) int resistanceLevel;
  @property (class, nonatomic, assign, readonly) int expendedEnergy;
  @property (class, nonatomic, assign, readonly) int heartRate;
  @property (class, nonatomic, assign, readonly) int metabolicEquivalent;
  @property (class, nonatomic, assign, readonly) int elapsedTime;
  @property (class, nonatomic, assign, readonly) int remainingTime;
  @property (class, nonatomic, assign, readonly) int singleEnergy;
  @property (class, nonatomic, assign, readonly) int pull;
  @property (class, nonatomic, assign, readonly) int thinkDragFactor;

  + (BOOL)hasFlag:(int)flags flag:(int)flag;

  @end

  @implementation RowerDataFlag

  + (BOOL)hasFlag:(int)flags flag:(int)flag {
      return (flags & flag) == flag;
  }

  + (int)moreData {
      return 1;
  }

  + (int)averageStrokeRate {
      return 2;
  }

  + (int)totalDistance {
      return 4;
  }

  + (int)instantaneousPace {
      return 8;
  }

  + (int)averagePace {
      return 16;
  }

  + (int)instantPower {
      return 32;
  }

  + (int)averagePower {
      return 64;
  }

  + (int)resistanceLevel {
      return 128;
  }

  + (int)expendedEnergy {
      return 256;
  }

  + (int)heartRate {
      return 512;
  }

  + (int)metabolicEquivalent {
      return 1024;
  }

  + (int)elapsedTime {
      return 2048;
  }

  + (int)remainingTime {
      return 4096;
  }

  + (int)singleEnergy {
      return 8192;
  }

  + (int)pull {
      return 16384;
  }

  + (int)thinkDragFactor {
      return 32768;
  }

  @end

  int flags = 465;

  if([RowerDataFlag hasFlag:flags flag:[RowerDataFlag moreData]]){
    NSLog(@"moreData flags : %u",flags);
  }

  if([RowerDataFlag hasFlag:flags flag:[RowerDataFlag totalDistance]]){
    NSLog(@"totalDistance flags : %u",flags);
  }

  if([RowerDataFlag hasFlag:flags flag:[RowerDataFlag averagePower]]){
    NSLog(@"averagePower flags : %u",flags);
  }

  ```

### DateTime
- #### DateTime format string 
  ```c#
  var str = DateTime.Now.ToString("yyyy-MM-dd HH:mm:ss.fff");
  ```
  ```objective-c
  NSDate *currentDate = [NSDate date];
  NSDateFormatter *dateFormatter = [[NSDateFormatter alloc] init];
  [dateFormatter setDateFormat:@"yyyy-MM-dd HH:mm:ss.SSS"];
  ```
