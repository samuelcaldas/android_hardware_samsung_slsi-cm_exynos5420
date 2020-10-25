r remaining input */
  memcpy(&context->buffer[bufindex], &input[i], inputLen-i);
}

/* MD4 padding. */
static void MD4Pad(MD4_CTX *context)
{
  unsigned char bits[8];
  unsigned int bufindex, padLen;

  /* Save number of bits */
  Encode (bits, context->count, 8);

  /* Pad out to 56 mod 64.
   */
  bufindex = (unsigned int)((context->count[0] >> 3) & 0x3f);
  padLen = (bufindex < 56) ? (56 - bufindex) : (120 - bufindex);
  MD4Update (context, PADDING, padLen);

  /* Append length (before padding) */
  MD4Update (context, bits, 8);
}

/* MD4 finalization. Ends an MD4 message-digest operation, writing the
     the message digest and zeroizing the context.
 */
static void MD4Final (unsigned char digest[16], MD4_CTX *context)
{
This file attempts to give generic guidelines on using RootPA. See from 
the .aidl files how to start up and use the services, from the .java 
files on details of particular components. Testing related information 
can be found from Locals/Test/Readme.txt.

When building RootPA, a rootpa-interface.jar is generated and copied to
Out/Bin/Release folder. This contains the com.gd.mobicore.pa.ifc 
package that is needed for implementing client that uses RootPA.

The actual RootPA is in RootPA-*.apk, * stands for release/debug 
signed/unsigned information. mdtest-RootPA*.apk contains RootPA that
uses MobiCore stub instead of real MobiCore. The stub accepts only 
some hardcoded values. Those can be found from Locals/Test/Readme.txt.


