---
title: Ban Appeals
extra_styles: form
---

It appears that you are currently in the server. In that case it would be easier to DM [@ModMail](https://discord.com/users/833145701701124116){: .mention target="_blank"}. Make sure to enable "Allow direct messages from server members".
{: #in_guild}

It appears that you are not currently in the server's ban list. If you are unable to join via the invite link [{{ site.data.links.discord_invite }}]({{ site.data.links.discord_invite }}){:target="_blank"}, continue with this form.
{: #not_in_banlist}

<!-- https://github.com/discord-math/bot/blob/main/plugins/appeals.py#L162 -->
<form action="{{ site.data.links.appeals_submit }}" method="post">
    <p>
        <legend>Do you know why you were banned?</legend>
        <input type="radio" name="type" id="clueless" value="clueless">
        <label for="clueless">No idea.</label><br />
        <input type="radio" name="type" id="compromised" value="compromised">
        <label for="compromised">My account was stolen/hacked/compromised.</label><br />
        <input type="radio" name="type" id="for_reason" value="for_reason" checked>
        <label for="for_reason">Yes:</label>
        <textarea id="reason" name="reason" placeholder="Why were you banned?" maxlength=4000></textarea>
    </p>
    <p>
        <label for="appeal">Why should you be unbanned?</label>
        <textarea name="appeal" placeholder="Why you should be unbanned?" maxlength=4000></textarea>
    </p>
    <p>
        We will send a friend request once your appeal is processed.
    </p>
    <input type="submit" class="button" value="Submit Appeal">
</form>
