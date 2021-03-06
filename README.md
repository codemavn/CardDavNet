CardDav.Net
======
C# .Net Implementation of the CardDav Client Protocol

Originally based off of:
https://raw.github.com/graviox/CardDAV-PHP/master/carddav.php

Written from the ground up in C#, with vCard Reader and Writer from: 
http://www.codeproject.com/Articles/16030/NET-vCard-API-for-creating-and-parsing-vCards

Thanks Lumi!

Though the vCard reader and writer needs to be updated to meet the new vCard 4.0 specification!

Be sure to replace the word username with the proper email account you are trying to access.

Simple usage for connecting to a CardDAV server:
```C#
using CardDav;
using CardDav.Card;
using CardDav.Response;

CardDav.Client client = new CardDav.Client("url of carddav server go here", "username", "some password");

CardDavResponse response = client.Get();

/** Output the results from the Listing **/

//Assuming you have a result text box to output too :P

resultsTxt.Text = response.ToString();

/** Set the client to the proper Address Book server URL **/
// This is heavily assumming that there are address books and vcards!
// Always check to see if CardDavResponse.AddressBooks.Count > 0
// And always check to see if CardDavResponse.Cards.Count > 0

client.SetServer(response.AddressBooks.First().Url.ToString());
vCard card = client.GetVCard(response.Cards.First().Id);

//Assuming you have a result text box to output too :P

resultsTxt.Text = resultsTxt.Text + "\r\n\r\n\r\n" + card.ToString();
```
To see a demo application compile and run the CardDavDemo project.

Google CardDAV API
------
To use this library against Google CardDAV API, you need to:  
1. authenticate using OAuth 2.0 by following [Google's instructions](https://developers.google.com/accounts/docs/OAuth2)  
2. supply the OAuth 2.0 access token you receive to the CardDav.Net constructor  
```C#
CardDav.Client client = new CardDav.Client("url of carddav server go here", "your OAuth 2.0 access token");
```
