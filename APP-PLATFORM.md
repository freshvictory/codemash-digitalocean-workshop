# 5. Introduction to App Platform

https://github.com/user-attachments/assets/8c0de1da-c15b-4762-a0f1-b933f8adc11e

## 5.1 Getting Started with DigitalOcean App Platform

1. Learn about the [App Platform](https://docs.digitalocean.com/products/app-platform/how-to/create-apps/) and its features.

## 5.2 Deploy Your First Application

1. Select **App Platform** from the DigitalOcean cloud console in the left sidebar.

    ![Select App Platform.](https://doimages.nyc3.cdn.digitaloceanspaces.com/GitHub/funko-showcase-workshop/5-AppPlatform/appplatform.png)

2. Click the **"Create App"** button.
3. Connect your GitHub account to the App Platform.
4. Once you connect your GitHub account, select the repository you want to deploy. This should be the project you've been working on.
5. The branch that is selected should be main and the source directory should be "/start". Leave **Autodeploy** checked. This will redeploy your site every time you push main to GitHub.
6. Click "Next".

## 5.3 Set Environment Variables
1. Click the "Edit" button next to Global.
    ![Click the Global Edit button.](https://doimages.nyc3.cdn.digitaloceanspaces.com/GitHub/funko-showcase-workshop/5-AppPlatform/envvars.png)
2. Click the "Bulk Editor" button.

    ![Click the bulk editor button.](https://doimages.nyc3.cdn.digitaloceanspaces.com/GitHub/funko-showcase-workshop/5-AppPlatform/bulkeditorbutton.png)

3. Copy the contents of your ".env" file you created earlier into the box.

    ![Copy your .env file into this box.](https://doimages.nyc3.cdn.digitaloceanspaces.com/GitHub/funko-showcase-workshop/5-AppPlatform/bulkeditor.png)

4. Click "Save".

    > **NOTE:** It is a best practice to encrypt your environment variables.  If your application is logging them, it will write their plain text to the logs if they are not encrypted.

5. Click "Next".
6. The `Info` screen shows your your app and region information. No changes needed here.  Click "Next".
7. Review your choices before deploying your new app.  No changes should be necessary.

    ![Review your choices.](https://doimages.nyc3.cdn.digitaloceanspaces.com/GitHub/funko-showcase-workshop/5-AppPlatform/appplatreview.png)

8. Click "Create Resources".  This will definitely take a few more minutes.  Time to hydrate?

## Fun Things To Do While You Wait

1. Click the `Go To Build Logs" button.  You can watch live as the server is configured and your app is deployed.
2. Once the Build is completed, you can also watch the Deploy Logs to watch the app spin up.

## 5.5 Access Your Running Application

- Once deployment has completed, visit the app's public URL to verify it's running correctly.

## 5.6 Make More Changes To Your Website!

1. It's time to go back to our local codebase and make some more meaningful changes to our UI.
2. In your `/start` directory, open the file `/components/FunkoCard/FunkoCard.tsx`.
3. You will see a code block that defines each of the "cards" for our collection items.  Currently, it only contains a ```<CardMedia/>``` tag, but we want to include the rest of the data from our database in this interface.
    ```html
    <Card sx={{ maxWidth: 345 }}>
        <CardMedia
        component="img"
        sx={{ height: 140 }}
        image={funko.imageUrl}
        alt={funko.character}
        />
    </Card>
    ```
4. After the ```<CardMedia/>``` tag, add a new, empty ```<CardContent></CardContent>``` node.
5. Inside the ```<CardContent>```, we can add our first text element: ```<Typography>```.  This a specific element from MaterialUI for rendering text.  If you haven't used MaterialUI before, that's OK.  [Here's some light reading about Material UI.](https://mui.com/material-ui/getting-started/?srsltid=AfmBOoqoiK0-bRTZdhwaq52_H7-h7zAHpItpfDzjnA4PaqZ09eOC9K0G)
6. Add the following line into your ```<CardContent>``` element. The `{funko.source}` is a reference to the data our app is pulling from the database earlier in the page.
    ```html
    <Typography gutterBottom variant="h2" component="div" sx={{ fontSize: '2em', fontWeight: 'bold' }}>{funko.source}</Typography>
    ```
7. Below that line, we can add another one for the character's name.
    ```html
    <Typography gutterBottom variant="h3" component="div" sx={{ fontSize: '1em' }}>{funko.character}</Typography>
    ```
8. There are two data properties left: `yearReleased` and `numberInLine`. These are less important, so we can use a smaller font for these.
    ```html
    <Typography variant="body2" color="text.secondary">Released: {funko.yearReleased}</Typography>
    <Typography variant="body2" color="text.secondary">Number in Line: {funko.numberInLine}</Typography>
    ```
9. Finally, we're going to give users the ability to edit items in their collection.  (We all make mistakes, right?)  We can add an Edit button at the bottom of each card. Since this is not technically `CardContent` but still part of the `Card`, we are going to put this element right after the closing `</CardContent>` tag.
    ```html
    <EditFunkoButton funko={funko} setFunkos={setFunkos} />
    ```
    > **NOTE:** If you ever get stuck, and can't fix your code, there's a copy of the entire app in the `/final` folder that is complete.  You can use those files if you need to fix something.
10. The Edit form and interface was already created for you, so after you rebuild and run your app again locally, you should see all of this functionality visible and working!
    ```bash
      npm run build
      npm run start
    ```
11. When you're happy with how your new cards appear, it's time for the AppPlat deployment magic. To best experience this, I recommend having a browser tab open to your AppPlat app. (It's the page where you watched the Build and Deploy logs earlier.)  When you're ready, commit your changes and push them to GitHub.
    ```bash
    git add .
    git commit -m "Initial commit"
    git push origin main
    ```
12. Now go watch that App Platform page!  It will automatically recognize that you made changes to your code, and auto-builds and auto-deploys them for you!  When it's done, you should see your new `Card` changes at your production URL!

→ [Next Up: Advanced Features](ADVANCED.md)
