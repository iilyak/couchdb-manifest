# Building couch

    repo init -u https://github.com/iilyak/couchdb-manifest.git
    repo sync

    # next step is only needed if you want to build a specific release
    repo init -b build-$BUILD -m release.xml

    wget https://raw.githubusercontent.com/iilyak/couchdb-manifest/master/rebar.config.script -O rebar.config.script.overwrite
    rebar -C rebar.config.script.overwrite compile

# Creating release


 1. Make sure you are on the master branch: repo init -b master
 2. Sync/checkout source, excluding local changes: repo sync --detach
 3. Generate a release manifest:

        repo manifest -r -o build-$BUILD.xml

    where $BUILD is the current release number
 4. Update release.xml:

        ln -sf build-$BUILD.xml release.xml

 5. Commit

        git add build-$BUILD.xml; git commit -a

 6. Tag

        git tag v$BUILD.$BRANCH.$PATCH

 7. Push

        git push origin HEAD:master HEAD:build-$BUILD v$BUILD.$BRANCH.$PATCH


Note the procedure and project structure is addapted from CoreOS
