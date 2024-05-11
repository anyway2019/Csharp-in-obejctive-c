# Csharp-in-obejctive-c

some Csharp api implemention in obejctive-c

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

### flags

### DateTime
