# How-to-intercept-the-message-created-in-SendMessage-event
SfChat allows to handle the messages in SendMessage event. Programmatically add the actual sent message into the Messages collection before adding the new message created in the event.

```
<sfChat:SfChat x:Name="sfChat"
               Messages="{Binding Messages}"
               SendMessage="SfChat_SendMessage"
               CurrentUser="{Binding CurrentUser}" />

```

```
private void SfChat_SendMessage(object sender, SendMessageEventArgs e)
{
  // Skips adding new message in Messages collection.
  e.Handled = true;

  // Now add the actual sent message into collection as required.
  this.sfChat.Messages.Add(e.Message);

  // You can add the special message into collection as like below.
  TextMessage textMessage = new TextMessage() { Author = sfChat.CurrentUser };
  textMessage.Text = "New message";
  this.sfChat.Messages.Add(textMessage);
}

```