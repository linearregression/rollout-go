# Rollout for Go/Zookeeper

## Usage

    zk, session, err := zookeeper.Dial("localhost:2181", 5e9)
    if err != nil {
        log.Fatal(err)
    }
    event := <-session
    if event.State != zookeeper.STATE_CONNECTED {
        log.Fatal("Cannot initialize zookeeper: ", event.State)
    }
    client := rollout.NewClient(zk, "/rollout/users")

    // The service must be started
    client.Start()

    // Check to see if this feature is enabled for this user
    client.FeatureActive("myfeature", userId, userGroups)

    // Don't forget to stop the service when you're done (usually on shutdown)
    client.Stop()
 

## Testing

You must have Zookeeper enabled on localhost:2181, then simply issue `make`.
